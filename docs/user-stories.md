# User Stories — ProxiVroum

## US1 — Publication d'un trajet (Conducteur)

**En tant que** Conducteaur,
**je veux** publier un trajet avec départ, destination, date, heure et nombre de places,
**afin de** proposer du covoiturage à des passagers sur mon itinéraire.

### Critère d'acceptation
- **Étant donné** qu'un conducteur est connecté,
- **Quand** il soumet un trajet valide,
- **Alors** le trajet apparaît dans les résultats de recherche dans les 30 secondes.

---

## US2 — Réservation d'une place (Passager)

**En tant que** Passager,
**je veux** réserver une place sur un trajet disponible et payer en ligne,
**afin de** confirmer mon transport de manière sécurisée.

### Critère d'acceptation
- **Étant donné** qu'un passager choisit un trajet et valide le paiement (PCI-DSS),
- **Quand** la transaction est acceptée,
- **Alors** le passager et le conducteur reçoivent une confirmation par email/notification.

---

## US3 — Notation après trajet (Passager)

**En tant que** Passager,
**je veux** noter le conducteur après un trajet terminé,
**afin de** contribuer à la confiance et la sécurité de la communauté.

### Critère d'acceptation
- **Étant donné** qu'un trajet est marqué comme terminé,
- **Quand** le passager soumet une note (1-5 étoiles),
- **Alors** la note est visible sur le profil du conducteur sous 5 minutes.
