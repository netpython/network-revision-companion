# 17 · BGP, attributs et politique de chemin

[Fiche précédente](../03-ip-et-routage/16-isis.md) · [Sommaire](../../README.md) · [Fiche suivante](../03-ip-et-routage/18-mp-bgp.md)

## Comprendre

BGP échange des informations de routage entre systèmes autonomes et au sein d'un AS. La session utilise TCP, avec le port serveur 179. eBGP et iBGP obéissent à des règles d'annonce et de next-hop différentes.

| Attribut | Usage de révision |
| --- | --- |
| AS_PATH | Chemin d'AS, prévention de boucles inter-AS |
| NEXT_HOP | Atteinte à résoudre avant l'utilisation du chemin |
| LOCAL_PREF | Préférence interne, valeur supérieure généralement préférée |
| MED | Indication de préférence d'entrée, comparaison dépendante des règles |
| Communities | Marqueurs utilisés par les politiques |

Un ordre de meilleur chemin précis dépend du constructeur, des options et des attributs disponibles. Weight est notamment un mécanisme local de certaines implémentations. Une règle apprise sur une plateforme ne doit pas être présentée comme universelle.

Une route peut être reçue puis filtrée, inéligible, non sélectionnée, ou sélectionnée sans gagner la RIB. Le next-hop doit être atteignable. Une origine configurée par network peut nécessiter un préfixe exact dans la RIB sur les implémentations concernées.

La réflexion de routes permet de réduire les exigences de maillage iBGP. Elle introduit des règles telles que ORIGINATOR_ID et CLUSTER_LIST et peut modifier la visibilité des chemins. Les préfixes autorisés, limites de routes et protections de session relèvent de la politique d'exploitation.

## Exemple concret

Un opérateur reçoit deux chemins pour 192.0.2.0/24. Il place LOCAL_PREF 200 sur le chemin souhaité et 100 sur l'autre. Dans les conditions de sélection applicables, la politique interne peut préférer le chemin à AS_PATH plus long.

## Pièges à éviter

- Réduire BGP au plus court AS_PATH.
- Confondre état Established et présence du préfixe utile.
- Comparer MED sans connaître les conditions de comparaison.

## Ce qu’il faut observer

Suivre le préfixe exact de l’annonce à la FIB. Lire AF/VRF, attributs, filtre, validité du next-hop et état du meilleur chemin.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

Pourquoi BGP est-il décrit comme protocole de politique ?

<details><summary>Afficher la correction</summary>

Les attributs et filtres permettent de choisir et contrôler la propagation au-delà d’une simple distance.

</details>

### Question 2

LOCAL_PREF est-il destiné à être envoyé normalement aux voisins eBGP ?

<details><summary>Afficher la correction</summary>

Il est utilisé à l’intérieur de l’AS, avec les règles définies pour cet attribut.

</details>

### Question 3

Une route non best est-elle nécessairement erronée ?

<details><summary>Afficher la correction</summary>

Non. Elle peut représenter un autre chemin valide non sélectionné.

</details>

## Sources pour approfondir

- [RFC 4271](https://www.rfc-editor.org/rfc/rfc4271)
- [RFC 4456](https://www.rfc-editor.org/rfc/rfc4456)
- [RFC 1997](https://www.rfc-editor.org/rfc/rfc1997)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
