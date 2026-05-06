# ProxiVroum

Plateforme de covoiturage régionale.

## Acteurs
- Conducteur, Passager, Modérateur, Service Comptabilité

## Fonctionnalités
- Publication de trajet, recherche, réservation, paiement
- Notation après trajet, support litige, stats modérateur, exports comptables

## Contraintes
- Disponibilité visée : 99,5 %
- Pic de charge : vendredi et dimanche soir
- Paiement conforme PCI-DSS
- Données personnelles conformes RGPD

## Structure du projet

```
proxivroum/
├── README.md
└── docs/
    ├── user-stories.md
    ├── criteres-qualite.md
    ├── use-case.puml
    ├── mcd.md
    ├── class-diagram.md
    └── adr/
        └── ADR-001-paiement.md
```
