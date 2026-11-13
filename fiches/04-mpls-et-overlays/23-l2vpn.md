# 23 · L2VPN, pseudowire, VPWS et VPLS

[Fiche précédente](../04-mpls-et-overlays/22-mpls-l3vpn.md) · [Sommaire](../../README.md) · [Fiche suivante](../04-mpls-et-overlays/24-vxlan.md)

## Comprendre

Une L2VPN transporte un service de liaison entre sites. Le client peut conserver ses propres mécanismes L3 au-dessus du service. Le fournisseur doit gérer l'identification des accès et la distribution des données dans son réseau.

| Service | Relation logique |
| --- | --- |
| VPWS | Service point à point |
| Pseudowire | Émulation d'un service de liaison au-dessus d'un transport |
| VPLS | Service Ethernet multipoint avec apprentissage MAC |
| EVPN | Plan de contrôle BGP applicable à des services Ethernet |

Un service point à point n'a pas les mêmes contraintes qu'un domaine Ethernet étendu multipoint. VPLS apprend les MAC et gère le trafic broadcast, unknown unicast et multicast, selon son architecture. Des règles de split horizon participent à la prévention de boucles.

Le service doit préciser l'encapsulation des accès, l'usage des tags, la MTU et les mécanismes de signalisation. La présence d'un pseudowire actif ne garantit pas que les VLANs client soient transportés comme attendu.

Étendre un domaine L2 augmente la portée des événements de broadcast, des déplacements MAC et de certaines erreurs. La séparation entre opérateur et client doit être claire pour l'observation et la restauration.

## Exemple concret

Deux CE s'attendent à échanger un VLAN tagué sur un service point à point. Si l'opérateur retire le tag d'un côté et le conserve de l'autre, le transport peut être actif tout en livrant une représentation incompatible du service.

## Pièges à éviter

- Assimiler toute L2VPN à VPLS.
- Supposer que le routage client est assuré par un service L2.
- Étendre un VLAN sans évaluer son domaine de panne.

## Ce qu’il faut observer

Vérifier état du service, labels ou encapsulation, mapping des accès, MAC apprises, taille des trames et traitement des tags.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

Quelle différence essentielle entre VPWS et VPLS ?

<details><summary>Afficher la correction</summary>

VPWS décrit un service point à point, VPLS une connectivité Ethernet multipoint.

</details>

### Question 2

Le client doit-il utiliser le routage de l’opérateur dans une L2VPN ?

<details><summary>Afficher la correction</summary>

Le service L2 permet au client de porter son propre routage au-dessus, selon le contrat.

</details>

### Question 3

Pourquoi vérifier BUM ?

<details><summary>Afficher la correction</summary>

Le trafic diffusé ou à destination inconnue peut être répliqué à grande échelle et révéler des boucles ou une mauvaise portée.

</details>

## Sources pour approfondir

- [RFC 4447](https://www.rfc-editor.org/rfc/rfc4447)
- [RFC 4762](https://www.rfc-editor.org/rfc/rfc4762)
- [RFC 7432](https://www.rfc-editor.org/rfc/rfc7432)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
