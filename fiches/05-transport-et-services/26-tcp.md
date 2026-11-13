# 26 · TCP, fiabilité, fenêtres et congestion

[Fiche précédente](../04-mpls-et-overlays/25-evpn.md) · [Sommaire](../../README.md) · [Fiche suivante](../05-transport-et-services/27-udp.md)

## Comprendre

TCP fournit un flux d'octets ordonné et fiable entre deux extrémités. Les numéros de séquence repèrent les octets et les ACK indiquent une progression de réception. Le transport ne conserve pas les frontières de messages applicatifs.

L'établissement classique utilise SYN, SYN-ACK, ACK. La fermeture ordonnée peut utiliser des FIN dans les deux sens, tandis qu'un RST interrompt une connexion. Les flags doivent être replacés dans le contexte de session.

| Mécanisme | Limitation concernée |
| --- | --- |
| Receive window | Capacité du récepteur à accepter des données |
| Congestion window | Contrôle de la charge injectée dans le réseau |
| Retransmission | Récupération de données non acquittées |
| SACK | Information sur des blocs reçus hors continuité |

Le volume envoyé dépend notamment des fenêtres disponibles et des données en vol. Une grande latence exige davantage de données en vol pour exploiter un débit donné. Le produit bande passante-délai fournit un ordre de grandeur, pas une garantie de performance.

Des retransmissions peuvent signaler pertes, réordonnancement ou effets de capture. Un ACK reçu n'atteste pas que l'application a traité ou enregistré les données. La négociation MSS et les options, comme window scaling, influencent la capacité d'échange.

## Exemple concret

À 100 Mbit/s et 100 ms de RTT, le produit débit-délai est environ 10 Mbit, soit 1,25 Mo. Une fenêtre réellement exploitable bien plus petite peut limiter le débit, même sur un lien non saturé.

## Pièges à éviter

- Attribuer chaque retransmission à un câble défectueux.
- Confondre receive window et congestion window.
- Assimiler connexion TCP établie et application fonctionnelle.

## Ce qu’il faut observer

Comparer handshake, RTT, séquences, ACK, retransmissions, fenêtres et sens des échanges. Connaître le point et les limites de capture.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

TCP transporte-t-il des messages avec des frontières conservées ?

<details><summary>Afficher la correction</summary>

Il fournit un flux d’octets. L’application définit ses propres messages.

</details>

### Question 2

Que signifie généralement le numéro ACK cumulatif ?

<details><summary>Afficher la correction</summary>

Le prochain numéro de séquence attendu de façon continue.

</details>

### Question 3

Pourquoi une faible fenêtre limite-t-elle un lien à grande latence ?

<details><summary>Afficher la correction</summary>

Elle réduit le volume pouvant rester en vol avant réception des acquittements.

</details>

## Sources pour approfondir

- [RFC 9293](https://www.rfc-editor.org/rfc/rfc9293)
- [RFC 5681](https://www.rfc-editor.org/rfc/rfc5681)
- [RFC 7323](https://www.rfc-editor.org/rfc/rfc7323)
- [RFC 2018](https://www.rfc-editor.org/rfc/rfc2018)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
