# 14 · OSPF, adjacencies, zones et LSA

[Fiche précédente](../03-ip-et-routage/13-rib-fib-et-selection.md) · [Sommaire](../../README.md) · [Fiche suivante](../03-ip-et-routage/15-eigrp.md)

## Comprendre

OSPF est un IGP à état de liens. Les voisins échangent des informations, synchronisent une LSDB et calculent des chemins avec SPF. OSPFv2 transporte l'IPv4, tandis qu'OSPFv3 et ses extensions prennent en charge des familles selon le déploiement.

Les zones limitent la portée des informations et des calculs. L'area 0 constitue le backbone d'une architecture multi-area standard. Un ABR relie des zones, un ASBR introduit des routes externes selon la politique.

| Repère OSPFv2 | Rôle de base |
| --- | --- |
| LSA 1 | Liens du routeur dans sa zone |
| LSA 2 | Réseau multi-accès représenté par le DR |
| LSA 3 | Préfixes inter-area |
| LSA 4 | Information d'atteinte d'un ASBR |
| LSA 5 / 7 | Routes externes / externes NSSA |

Sur un segment broadcast, DR et BDR réduisent les adjacencies complètes nécessaires. Deux DROTHER peuvent rester en 2-WAY. EXSTART/EXCHANGE concernent la négociation et l'échange de base, et ne désignent pas à eux seuls une cause précise.

Les timers, zone, paramètres d'authentification et type de réseau influencent l'adjacency. Une différence de MTU peut bloquer la synchronisation. Les interfaces passives restent annonçables tout en supprimant les échanges de voisinage associés. Les zones stub et NSSA modifient les types d'informations admises.

## Exemple concret

R1 en area 0 rejoint R3 en area 10 via R2 ABR. Le préfixe de R3 apparaît comme inter-area chez R1. Voir le voisin FULL ne suffit pas à prouver que ce préfixe précis est annoncé et installé.

## Pièges à éviter

- Considérer 2-WAY comme toujours anormal.
- Déduire un problème de MTU de tout état EXSTART.
- Confondre LSDB complète et forwarding applicatif correct.

## Ce qu’il faut observer

Comparer paramètres des deux interfaces, rôle DR/BDR, état de voisin, LSA du préfixe et RIB. Corréler les événements physiques aux transitions.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

Que calcule SPF ?

<details><summary>Afficher la correction</summary>

Les chemins à partir de la base d’état de liens du domaine considéré.

</details>

### Question 2

Une interface passive peut-elle être annoncée ?

<details><summary>Afficher la correction</summary>

Oui, selon sa participation au processus et la configuration.

</details>

### Question 3

Quel routeur introduit généralement des routes d’un autre domaine dans OSPF ?

<details><summary>Afficher la correction</summary>

Un ASBR, selon les règles de redistribution et de zone.

</details>

## Sources pour approfondir

- [RFC 2328](https://www.rfc-editor.org/rfc/rfc2328)
- [RFC 5340](https://www.rfc-editor.org/rfc/rfc5340)
- [RFC 3101](https://www.rfc-editor.org/rfc/rfc3101)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
