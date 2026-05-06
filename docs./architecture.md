---

## 3. Explications détaillées

### 3.1 Pourquoi ces Bounded Contexts ?

- **Trajet** : recherche forte volumétrie (pic vendredi/dimanche) → scalabilité horizontale possible.
- **Réservation** : cohérence transactionnelle forte (pas de surréservation).
- **Paiement** : isolation PCI-DSS, audits ciblés.
- **Notation** : peut être asynchrone, pas bloquant pour le paiement.
- **Support & Litige** : règles spécifiques (délais, preuves, rôle modérateur).

### 3.2 Clean Architecture dans le diagramme

| Couche | Rôle | Exemple dans le diagramme |
|--------|------|---------------------------|
| **Entities** | Règles métier fondamentales, indépendantes de tout détail | `Trajet`, `Reservation`, `Transaction` |
| **Use Cases** | Orchestration des entités pour répondre aux besoins utilisateur | `UC_Reserver`, `UC_Publier` |
| **Interface Adapters** | Traduction entre le monde extérieur et les use cases | `Controller`, `RepoImpl`, `Gateway` |
| **Frameworks & Drivers** | Détails techniques : bases de données, API, messages | `PostgreSQL`, `Redis`, `Kafka` |

Les dépendances vont **toujours de l’extérieur vers l’intérieur** (flèches dans le diagramme).  
Les use cases ne connaissent pas la base de données ni l’API.

### 3.3 Avantages pour ProxiVroum

- **Testabilité** : chaque use case peut être testé sans base de données réelle ni API.
- **Évolution** : remplacer PostgreSQL par un autre SGBD sans toucher au métier.
- **PCI-DSS** : le bounded context Paiement peut avoir son propre déploiement.
- **RGPD** : la suppression d’un utilisateur se propage proprement en traversant les use cases.

---

## 4. Code à copier dans ton dépôt

Crée un fichier `docs/EXERCICE3.md` avec :

```markdown
# Exercice 3 – Architecture cible

## Bounded Contexts

| Bounded Context | Responsabilité |
|----------------|----------------|
| Trajet | Publication et recherche de trajets |
| Réservation | Gestion des réservations |
| Paiement | Transactions financières (PCI-DSS) |
| Notation | Avis post-trajets |
| Support & Litige | Gestion des conflits |

## Diagramme de composants (Clean Architecture)

```mermaid
flowchart TB
    subgraph "Frameworks & Drivers (Couche externe)"
        API[REST API / GraphQL]
        DB[(PostgreSQL)]
        Redis[(Redis Cache)]
        Queue[Message Queue / Kafka]
        ExtPaiement[Paiement externe\nStripe/Lyra]
    end

    subgraph "Interface Adapters"
        Controller[Contrôleurs HTTP]
        Presenter[Présentateurs / DTO]
        RepoImpl[Implémentations Repository]
        Gateway[Gateway Paiement]
        Subscriber[Subscriber Kafka]
    end

    subgraph "Application Business Rules (Use Cases)"
        UC_Reserver["Réserver un trajet"]
        UC_Publier["Publier un trajet"]
        UC_Annuler["Annuler réservation"]
        UC_Noter["Noter après trajet"]
        UC_Litige["Ouvrir un litige"]
    end

    subgraph "Enterprise Business Rules (Entities)"
        Trajet
        Reservation
        Utilisateur
        Transaction
        Avis
        Litige
    end

    API --> Controller
    Controller --> UC_Reserver
    Controller --> UC_Publier
    Controller --> UC_Annuler
    Controller --> UC_Noter
    Controller --> UC_Litige

    UC_Reserver --> Reservation
    UC_Reserver --> Trajet
    UC_Publier --> Trajet
    UC_Annuler --> Reservation
    UC_Noter --> Avis
    UC_Litige --> Litige
    UC_Litige --> Reservation

    UC_Reserver --> RepoImpl
    UC_Publier --> RepoImpl
    RepoImpl --> DB
    RepoImpl --> Redis

    UC_Reserver --> Gateway
    Gateway --> ExtPaiement

    Subscriber --> Queue
    Subscriber --> UC_Noter
