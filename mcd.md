# MCD — ProxiVroum

## Entités et relations

```mermaid
erDiagram
  UTILISATEUR ||--o{ VEHICULE : possède
  UTILISATEUR ||--o{ TRAJET : publie
  UTILISATEUR ||--o{ RESERVATION : fait
  UTILISATEUR ||--o{ LITIGE : ouvre
  VEHICULE }o--|| TRAJET : "utilisé dans"
  TRAJET ||--o{ RESERVATION : concerne
  RESERVATION ||--|| PAIEMENT : génère
  RESERVATION ||--o| NOTATION : évalue
  RESERVATION ||--o| LITIGE : concerne

  UTILISATEUR { uuid id PK string nom string email string telephone string statut }
  VEHICULE { uuid id PK string marque string modele string immatriculation int nb_places }
  TRAJET { uuid id PK string ville_depart string ville_arrivee datetime date_heure int nb_places float prix }
  RESERVATION { uuid id PK datetime date_reservation string statut int nb_places }
  PAIEMENT { uuid id PK float montant datetime date_paiement string statut string ref_stripe }
  NOTATION { uuid id PK int note string commentaire datetime date_notation }
  LITIGE { uuid id PK string description string statut datetime date_ouverture }
```

## Vérification 3NF
- **1FN** : toutes les valeurs sont atomiques
- **2FN** : chaque attribut dépend de toute la clé primaire
- **3FN** : aucune dépendance transitive entre attributs non-clés
