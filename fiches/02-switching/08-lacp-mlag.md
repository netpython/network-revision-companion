# 08 · LACP, port-channel et MLAG

[Fiche précédente](../02-switching/07-pvst-rapid-pvst.md) · [Sommaire](../../README.md) · [Fiche suivante](../02-switching/09-lldp-et-decouverte.md)

## Comprendre

Une agrégation rassemble plusieurs liens physiques dans une interface logique. LACP négocie l'appartenance au groupe et échange les informations d'acteur et de partenaire. Le mode active initie les échanges, passive attend une sollicitation. Deux côtés passive ne forment pas un groupe LACP.

Le trafic est distribué par un algorithme de sélection, souvent fondé sur des champs MAC, IP et éventuellement L4. Un flux individuel suit généralement un seul membre afin de préserver l'ordre. Additionner les débits des liens ne donne donc pas le débit accessible par un flux unique.

| Observation | Interprétation à confirmer |
| --- | --- |
| Membre bundled | Participe à l'agrégat |
| Individual / suspended | Pas de participation normale à l'agrégat |
| Débit déséquilibré | Peut résulter du hash et du nombre de flux |

Le groupe doit présenter des caractéristiques compatibles, notamment VLAN, vitesse et paramètres exigés par la plateforme. L'interface logique porte le rôle attendu dans la topologie.

MLAG, vPC et technologies apparentées permettent à deux châssis de présenter un agrégat commun à un voisin. Elles ajoutent des mécanismes de synchronisation et de contrôle de double-actif propres au produit. LACP seul ne fournit pas cette coordination multi-châssis.

## Exemple concret

Deux liens de 10 Gbit/s forment un port-channel. Plusieurs flux peuvent exploiter 20 Gbit/s agrégés en conditions favorables. Un transfert unique peut rester limité à un membre de 10 Gbit/s.

## Pièges à éviter

- Attendre un doublement automatique du débit d’un flux.
- Configurer une agrégation entre deux châssis sans technologie multi-châssis compatible.
- Confondre lien physique up et membre sélectionné.

## Ce qu’il faut observer

Vérifier système partenaire, état des membres, cohérence VLAN, hash et dépendances de pair pour MLAG.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

Active/passive peut-il fonctionner ?

<details><summary>Afficher la correction</summary>

Oui. Le côté active initie la négociation.

</details>

### Question 2

LACP active/active fonctionne-t-il ?

<details><summary>Afficher la correction</summary>

Oui, sous réserve de compatibilité des paramètres et de la topologie.

</details>

### Question 3

Pourquoi un agrégat à deux liens peut-il être déséquilibré ?

<details><summary>Afficher la correction</summary>

Le hash répartit des flux, dont la taille et le nombre ne sont pas nécessairement uniformes.

</details>

## Sources pour approfondir

- [Documentation de référence 1](https://1.ieee802.org/tsn/802-1ax-rev/)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
