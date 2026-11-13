# 24 · VXLAN, VTEP, VNI et underlay

[Fiche précédente](../04-mpls-et-overlays/23-l2vpn.md) · [Sommaire](../../README.md) · [Fiche suivante](../04-mpls-et-overlays/25-evpn.md)

## Comprendre

VXLAN encapsule une trame Ethernet dans UDP/IP afin de transporter un segment logique au-dessus d'un réseau IP. Les VTEP réalisent l'encapsulation et la décapsulation. Le VNI fournit un identifiant de segment sur 24 bits.

| Plan | Responsabilité |
| --- | --- |
| Underlay | Joindre les adresses IP de tunnel des VTEP |
| Overlay | Identifier les segments et leurs destinations |
| Contrôle | Apprendre ou distribuer les informations utiles |
| Données | Transporter les trames encapsulées |

Le port destination UDP VXLAN enregistré est 4789. Le port source peut aider à répartir les flux dans le réseau IP. L'underlay peut alors utiliser ECMP sans apprendre les MAC des clients.

Pour un paquet IP client de 1500 octets encapsulé dans Ethernet sans tag intérieur, le paquet IP extérieur IPv4 atteint typiquement 1550 octets. L'équivalent IPv6 extérieur atteint 1570 octets. Ces exemples ajoutent Ethernet intérieur, VXLAN, UDP et IP extérieur. Les tags supplémentaires ou autres encapsulations changent le calcul.

VXLAN définit le transport, pas l'ensemble de son contrôle. L'apprentissage peut être fondé sur le plan de données ou un mécanisme de contrôle tel qu'EVPN. Le traitement BUM dépend de la réplication configurée.

## Exemple concret

VTEP-A peut joindre VTEP-B par ping avec de petits paquets. Les échanges clients volumineux échouent parce que l'underlay accepte 1500 octets, alors que l'IP extérieur en exige 1550 dans ce cas.

## Pièges à éviter

- Considérer VXLAN et EVPN comme un seul protocole.
- Dimensionner uniquement la MTU IP des hôtes.
- Confondre VLAN local et VNI global du service.

## Ce qu’il faut observer

Vérifier joignabilité VTEP, source de tunnel, VNI, mapping VLAN, réplication et MTU réelle sur le chemin.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

Le VNI remplace-t-il toutes les politiques de sécurité ?

<details><summary>Afficher la correction</summary>

Non. Il identifie un contexte de segment, tandis que l’accès et le filtrage doivent être conçus.

</details>

### Question 2

Quel rôle joue le VTEP ?

<details><summary>Afficher la correction</summary>

Il ajoute ou retire l’encapsulation VXLAN.

</details>

### Question 3

Pourquoi un ping VTEP réussi peut-il être insuffisant ?

<details><summary>Afficher la correction</summary>

Il ne prouve ni la taille de paquet nécessaire ni le mapping et le forwarding du service client.

</details>

## Sources pour approfondir

- [RFC 7348](https://www.rfc-editor.org/rfc/rfc7348)
- [RFC 8365](https://www.rfc-editor.org/rfc/rfc8365)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
