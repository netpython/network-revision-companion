# 29 · DHCP, DNS et NTP comme dépendances réseau

[Fiche précédente](../05-transport-et-services/28-mtu-mss-pmtud.md) · [Sommaire](../../README.md) · [Fiche suivante](../05-transport-et-services/30-nat-pat.md)

## Comprendre

Ces services dépassent L4 dans le modèle fonctionnel, mais ils déterminent de nombreuses perceptions de panne réseau. Les traiter complète la lecture des couches inférieures.

| Service | Rôle | Transports usuels |
| --- | --- | --- |
| DHCPv4 | Paramètres d'hôte et bail | UDP 67/68 |
| DNS classique | Résolution et données de noms | UDP et TCP 53 |
| NTP | Synchronisation de temps | UDP 123 |

DHCPv4 utilise généralement Discover, Offer, Request et ACK. Un relais reçoit les broadcasts d'un LAN et transmet vers le serveur. L'adresse giaddr aide au choix du pool. Des exclusions réservent des adresses et les baux définissent une durée, pas une garantie de permanence.

DNS sépare résolution récursive, autorités et caches. TTL DNS exprime la durée de conservation admissible d'un enregistrement, distincte du TTL d'un paquet IP. NXDOMAIN, SERVFAIL et timeout ne décrivent pas la même situation. DNS peut aussi être transporté par des protocoles chiffrés supplémentaires.

NTP aide à aligner les horloges. La qualité de synchronisation, les sources et la confiance dans le temps influencent la corrélation d'événements, les certificats et certaines authentifications. Des timestamps affichés dans des fuseaux différents doivent être normalisés.

## Exemple concret

Un service fonctionne par adresse mais échoue par nom. La réponse DNS, la famille A/AAAA choisie et le traitement applicatif doivent être examinés. Un test HTTPS par IP peut aussi changer Host/SNI et ne pas constituer un témoin équivalent.

## Pièges à éviter

- Assimiler NXDOMAIN et absence de réponse.
- Oublier TCP 53 dans une politique DNS classique.
- Corréler des logs sans contrôler fuseaux et dérive d’horloge.

## Ce qu’il faut observer

Vérifier bail et options, résolveur réellement interrogé, nom/type exacts, réponse DNS, état NTP et référence horaire des journaux.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

À quoi sert giaddr dans un relais DHCPv4 ?

<details><summary>Afficher la correction</summary>

Il indique notamment le sous-réseau de relais permettant au serveur de choisir le pool.

</details>

### Question 2

TTL DNS et TTL IP ont-ils la même fonction ?

<details><summary>Afficher la correction</summary>

Non. L’un concerne le cache de données DNS, l’autre la durée de vie en sauts d’un paquet IP.

</details>

### Question 3

Pourquoi tester A et AAAA ?

<details><summary>Afficher la correction</summary>

Le client peut choisir une famille dont le chemin ou la politique diffère.

</details>

## Sources pour approfondir

- [RFC 2131](https://www.rfc-editor.org/rfc/rfc2131)
- [RFC 1034](https://www.rfc-editor.org/rfc/rfc1034)
- [RFC 1035](https://www.rfc-editor.org/rfc/rfc1035)
- [RFC 7766](https://www.rfc-editor.org/rfc/rfc7766)
- [RFC 5905](https://www.rfc-editor.org/rfc/rfc5905)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
