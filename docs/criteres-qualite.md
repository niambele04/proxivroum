# Critères de Qualité — ProxiVroum

## CQ1 — Disponibilité (Fiabilité)

Le système doit être disponible **99,5 % du temps** mesuré sur un mois glissant,
y compris lors des pics du vendredi et dimanche soir (18h–23h).

**Mesure :** Uptime monitoring (ex. Datadog, UptimeRobot)
— alertes si downtime > 3,6h/mois.

---

## CQ2 — Performance sous charge

Le temps de réponse de la recherche de trajets doit être
**< 1 seconde au P95** lors des pics de charge
(simulation de 500 utilisateurs simultanés).

**Mesure :** Tests de charge avec k6 ou JMeter
— rapport P95/P99 à chaque déploiement.

---

## CQ3 — Conformité RGPD / Sécurité

100 % des données personnelles (nom, email, téléphone) doivent être
**chiffrées au repos et en transit**, et supprimables sur demande en **< 72h**.

**Mesure :** Audit de conformité + test automatisé de la route
`DELETE /user/{id}` en CI/CD.
