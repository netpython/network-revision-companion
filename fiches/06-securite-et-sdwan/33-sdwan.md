# 33 · SD-WAN, underlay, overlay et politique applicative

[Fiche précédente](../06-securite-et-sdwan/32-acl-firewall-ipsec.md) · [Sommaire](../../README.md) · [Fiche suivante](../07-acces-et-wifi/34-nac.md)

## Comprendre

Le SD-WAN organise la connectivité WAN au moyen de politiques et de fonctions de contrôle centralisées ou orchestrées. Il combine des transports disponibles avec un overlay et des décisions de chemin adaptées aux services.

| Plan | Question principale |
| --- | --- |
| Underlay | Les extrémités peuvent-elles se joindre sur chaque transport ? |
| Contrôle | Quelles routes et politiques sont distribuées ? |
| Données | Quels tunnels transfèrent réellement le trafic ? |
| Gestion | Comment provisionner, observer et maintenir le réseau ? |

Les liens peuvent utiliser Internet, MPLS opérateur ou d'autres accès. Deux liens de technologies différentes peuvent partager un même risque physique ou opérateur. Une diversité affichée ne prouve pas une indépendance réelle.

Les mesures de perte, latence et gigue alimentent des politiques selon les capacités du produit. Le chemin choisi dépend aussi de la classification du trafic, de la disponibilité des routes et des préférences. BFD peut contribuer à surveiller les chemins. Les noms et rôles précis varient entre fournisseurs.

Dans Cisco Catalyst SD-WAN, OMP est notamment utilisé pour distribuer les informations de contrôle, tandis que des tunnels assurent le transport des données. Il faut distinguer ce cas produit du concept général SD-WAN.

La bascule doit considérer l'état des sessions, le NAT, le retour, les seuils et les temporisations. Des changements trop fréquents peuvent affecter les applications.

## Exemple concret

Deux transports sont up. L'un présente des pertes dépassant le seuil d'une politique voix. L'overlay peut déplacer les nouveaux flux ou appliquer une autre décision selon le produit. Il faut vérifier la règle et le comportement réel des sessions.

## Pièges à éviter

- Confondre présence du contrôleur et bon état de chaque tunnel.
- Réduire le choix de chemin au débit annoncé.
- Généraliser les noms de composants d’un fournisseur à tous les SD-WAN.

## Ce qu’il faut observer

Vérifier transports, sessions de contrôle, routes distribuées, tunnels, sondes et règle appliquée au flux. Observer aussi le retour.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

Un tunnel up garantit-il le respect du SLA applicatif ?

<details><summary>Afficher la correction</summary>

Non. La qualité mesurée et les critères de la politique doivent être comparés.

</details>

### Question 2

Deux accès différents garantissent-ils la diversité physique ?

<details><summary>Afficher la correction</summary>

Non. Ils peuvent partager un chemin ou un point de panne.

</details>

### Question 3

Pourquoi un diagnostic SD-WAN doit-il commencer par l’underlay ?

<details><summary>Afficher la correction</summary>

L’overlay dépend d’une joignabilité et de caractéristiques de transport sous-jacentes.

</details>

## Sources pour approfondir

- [Documentation de référence 1](https://www.cisco.com/c/en/us/td/docs/routers/sdwan/26x-later/solution/cisco-catalyst-sd-wan-solution-overview/solution.html)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
