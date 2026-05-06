# Architecture cible — ProxiVroum

## Bounded Contexts

| Contexte | Responsabilité |
|---|---|
| Trajet | Publication, recherche, gestion des trajets (service central) |
| Réservation | Réservation et annulation de places |
| Paiement | Traitement Stripe, remboursements, exports comptables |
| Notation | Avis et calcul de confiance |
| Litige | Support et modération |
| Identité | Authentification et gestion des profils |

## Clean Architecture — service Trajet

```
┌─────────────────────────────────────┐
│         PRESENTATION                │
│  REST API · Event listeners · Auth  │
├─────────────────────────────────────┤
│         APPLICATION                 │
│  PublierTrajetCmd · RechercherQ     │
├─────────────────────────────────────┤
│         DOMAIN  ← noyau             │
│  Trajet · Prix · TrajetRepository   │
│  TrajetPubliéEvent                  │
├─────────────────────────────────────┤
│         INFRASTRUCTURE              │
│  PostgreSQL · Redis · Kafka · Maps  │
└─────────────────────────────────────┘
```

> Règle de dépendance : les couches externes dépendent toujours du Domain, jamais l'inverse.
