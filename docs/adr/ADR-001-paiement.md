# ADR-001 — Choix de l'architecture de paiement

## Statut
Accepté

## Contexte
ProxiVroum doit gérer des paiements en ligne conformes PCI-DSS,
avec des pics de charge le vendredi et dimanche soir.
Implémenter soi-même un système de paiement est long, risqué
et coûteux en certification.

## Décision
Utiliser un prestataire de paiement tiers **(Stripe)** via son API,
sans jamais faire transiter les données de carte bancaire
par nos propres serveurs.

## Alternatives considérées

| Option | Avantage | Inconvénient |
|---|---|---|
| Stripe (choix retenu) | Certifié PCI-DSS, rapide à intégrer, scalable | Coût par transaction (~1,4%) |
| Paiement maison | Contrôle total | Certification PCI-DSS très coûteuse, risque élevé |
| PayPal | Connu des utilisateurs | UX moins fluide, API moins flexible |

## Conséquences

Aucune donnée bancaire stockée sur nos serveurs → conformité PCI-DSS garantie

Scalabilité gérée par Stripe pendant les pics

Dépendance à un fournisseur externe

Commission à intégrer dans le modèle économique
