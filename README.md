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
    ├── adr/
        └── ADR-001-paiement.md
    ├── class-diagram.md
    ├── criteres-qualite.md
    ├── mcd.md
    ├── use-case.puml  
    └──user-stories.md
 
```
