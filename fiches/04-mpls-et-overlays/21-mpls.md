# 21 · MPLS, labels et transport

[Fiche précédente](../03-ip-et-routage/20-vrf.md) · [Sommaire](../../README.md) · [Fiche suivante](../04-mpls-et-overlays/22-mpls-l3vpn.md)

## Comprendre

MPLS associe des paquets à une Forwarding Equivalence Class, puis permet leur transfert à l'aide de labels. Les équipements peuvent ajouter, remplacer ou retirer un label. La décision reste liée à un état de contrôle installé.

| Opération | Effet |
| --- | --- |
| Push | Ajout d'un ou plusieurs labels |
| Swap | Remplacement du label utilisé pour le transfert |
| Pop | Retrait du label supérieur |
| PHP | Retrait du label de transport par l'avant-dernier saut lorsque prévu |

Un élément de pile MPLS comporte 20 bits de label, 3 bits de Traffic Class, un bit de fond de pile et un TTL. Plusieurs labels peuvent coexister, avec des fonctions différentes. Le label a généralement une signification locale au contexte où il est reçu.

LDP distribue des associations entre FEC et labels dans des architectures courantes. D'autres mécanismes, comme BGP ou Segment Routing, peuvent porter des informations nécessaires à d'autres types de LSP. MPLS ne signifie donc pas obligatoirement LDP.

Un label de transport permet d'atteindre une extrémité de service. Un label supplémentaire peut identifier le traitement du service à l'arrivée. Il faut dimensionner la MTU pour la pile. MPLS offre une séparation ou un transport de services, sans garantir leur chiffrement.

## Exemple concret

Un PE ajoute un label de transport vers le PE distant et un label de service VPN. Les routeurs de transit examinent le label supérieur. Le PE de sortie utilise le label de service pour déterminer le traitement client.

## Pièges à éviter

- Croire qu’un même numéro de label désigne forcément le même service dans tout le réseau.
- Assimiler MPLS à un mécanisme de chiffrement.
- Vérifier le seul IGP en oubliant la distribution et l’installation des labels.

## Ce qu’il faut observer

Suivre route de transport, FEC, next-hop, label entrant/sortant et MTU. Vérifier séparément le transport et le service.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

Quelle taille fait un élément de pile MPLS ?

<details><summary>Afficher la correction</summary>

Quatre octets.

</details>

### Question 2

À quoi sert le bit S ?

<details><summary>Afficher la correction</summary>

À identifier le fond de pile de labels.

</details>

### Question 3

MPLS nécessite-t-il toujours LDP ?

<details><summary>Afficher la correction</summary>

Non. La distribution ou le choix des labels peut reposer sur d’autres mécanismes selon l’architecture.

</details>

## Sources pour approfondir

- [RFC 3031](https://www.rfc-editor.org/rfc/rfc3031)
- [RFC 3032](https://www.rfc-editor.org/rfc/rfc3032)
- [RFC 5036](https://www.rfc-editor.org/rfc/rfc5036)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
