# 28 · MTU, MSS, fragmentation et PMTUD

[Fiche précédente](../05-transport-et-services/27-udp.md) · [Sommaire](../../README.md) · [Fiche suivante](../05-transport-et-services/29-dhcp-dns-ntp.md)

## Comprendre

La MTU décrit une taille maximale à un niveau donné. L'IP MTU désigne la taille du paquet IP sur un lien. Les limites de trame Ethernet, l'IP intérieur et l'IP extérieur d'un tunnel doivent être distingués.

MSS limite la taille de données TCP qu'une extrémité annonce accepter par segment. Pour IP MTU 1500, les valeurs simples de 1460 en IPv4 et 1440 en IPv6 supposent les en-têtes IP/TCP de base. Les options et extensions changent l'espace disponible.

| Fonction | IPv4 | IPv6 |
| --- | --- | --- |
| Fragmentation en transit | Possible si les conditions le permettent, dont DF | Pas par les routeurs |
| Signal de MTU insuffisante | ICMP fragmentation needed | ICMPv6 Packet Too Big |
| Adaptation | Source et PMTUD selon pile | Source et PMTUD selon pile |

PMTUD apprend les contraintes du chemin à partir des retours nécessaires. PLPMTUD utilise une logique de sondage au niveau du transport pour réduire certaines dépendances au retour ICMP. Un filtrage inadapté peut produire un trou noir de MTU.

Ajuster MSS concerne TCP et ne corrige pas tous les usages UDP ou les encapsulations. Un tunnel consomme une partie de la capacité du paquet extérieur. Le calcul doit préciser exactement quels en-têtes et tags sont ajoutés.

## Exemple concret

Un VPN transporte un petit ping, mais les transferts TCP bloquent après le handshake. Les premiers messages sont petits. Il faut tester la taille exploitable et les retours de PMTUD avant de conclure que le tunnel est sain.

## Pièges à éviter

- Confondre MTU IP et taille de trame sur le fil.
- Appliquer un MSS clamp comme correction générale de tout trafic.
- Comparer des tailles ping entre outils sans vérifier ce qu’elles représentent.

## Ce qu’il faut observer

Mesurer des tailles explicites, DF si applicable, retours ICMP et en-têtes d’encapsulation. Vérifier aller et retour.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

Pourquoi un handshake peut-il passer avant un blocage de transfert ?

<details><summary>Afficher la correction</summary>

Les paquets de contrôle peuvent être plus petits que les paquets de données qui dépassent la MTU.

</details>

### Question 2

MSS s’applique-t-il à UDP ?

<details><summary>Afficher la correction</summary>

Non. MSS est une option TCP.

</details>

### Question 3

Une IP MTU extérieure de 1500 garantit-elle 1500 pour l’IP intérieur ?

<details><summary>Afficher la correction</summary>

Non. L’encapsulation consomme de la place.

</details>

## Sources pour approfondir

- [RFC 1191](https://www.rfc-editor.org/rfc/rfc1191)
- [RFC 8201](https://www.rfc-editor.org/rfc/rfc8201)
- [RFC 8899](https://www.rfc-editor.org/rfc/rfc8899)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
