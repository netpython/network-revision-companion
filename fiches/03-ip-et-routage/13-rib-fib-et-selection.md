# 13 · RIB, FIB et choix de route

[Fiche précédente](../03-ip-et-routage/12-arp-nd-icmp.md) · [Sommaire](../../README.md) · [Fiche suivante](../03-ip-et-routage/14-ospf.md)

## Comprendre

La RIB regroupe des routes issues de sources comme connecté, statique ou protocoles de routage. La FIB contient les informations utilisées pour le forwarding. Selon le produit, des tables matérielles et des adjacencies complètent cette installation.

La sélection suit plusieurs décisions distinctes. Un protocole choisit ses candidats selon sa logique. Pour un même préfixe, la préférence administrative du système départage les sources. Le forwarding cherche ensuite le préfixe installé le plus spécifique correspondant à la destination.

| Notion | Question |
| --- | --- |
| Métrique | Quel candidat le protocole préfère-t-il ? |
| Distance/préférence administrative | Quelle source de route est préférée pour ce préfixe ? |
| Longest prefix match | Quelle entrée de forwarding couvre le plus précisément la destination ? |
| Résolution récursive | Comment atteindre le next-hop annoncé ? |

La distance administrative et ses valeurs par défaut dépendent du constructeur. Une métrique OSPF n'est pas directement comparable à une métrique EIGRP. Une route présente en BGP peut ne pas gagner la RIB, puis ne pas être installée comme attendu.

ECMP permet plusieurs next-hops de coût considéré égal. Leur nombre maximal et leur répartition dépendent du système. Une route par défaut /0 est utilisée en l'absence de route plus spécifique admissible.

## Exemple concret

Une route /24 via OSPF et une route /25 statique sont toutes deux installées. Pour une destination du /25, le forwarding utilise le /25. La comparaison de distances entre sources d'un même préfixe ne remplace pas le longest prefix match.

## Pièges à éviter

- Comparer des métriques de protocoles différents comme une échelle commune.
- Croire qu’une route visible dans une base protocolaire est forcément dans la FIB.
- Confondre sélection de source pour un préfixe et recherche du plus long préfixe.

## Ce qu’il faut observer

Partir d’une destination précise et de la bonne VRF. Lire RIB, FIB, résolution de next-hop, adjacency et politique de routage éventuelle.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

Une route /0 gagne-t-elle contre une /24 qui couvre la destination ?

<details><summary>Afficher la correction</summary>

Non, si la /24 est installée et admissible, elle est plus spécifique.

</details>

### Question 2

Qu’est-ce qu’un next-hop récursif ?

<details><summary>Afficher la correction</summary>

Un next-hop dont l’atteinte doit être résolue par une autre entrée de routage.

</details>

### Question 3

Pourquoi RIB et FIB peuvent-elles diverger ?

<details><summary>Afficher la correction</summary>

Une installation peut échouer, être limitée ou ne pas utiliser la route candidate considérée.

</details>

## Sources pour approfondir

- [RFC 1812](https://www.rfc-editor.org/rfc/rfc1812)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
