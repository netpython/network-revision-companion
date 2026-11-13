# 19 · Redistribution, filtrage et prévention des boucles

[Fiche précédente](../03-ip-et-routage/18-mp-bgp.md) · [Sommaire](../../README.md) · [Fiche suivante](../03-ip-et-routage/20-vrf.md)

## Comprendre

Redistribuer consiste à injecter des routes provenant d'une source dans un autre protocole. L'opération change le domaine de propagation et parfois les attributs servant à la sélection.

La métrique de la source n'est pas automatiquement équivalente à celle de la cible. Il faut définir les préfixes concernés, la métrique initiale, le type de route externe et les contraintes propres au protocole.

| Mécanisme | Utilité |
| --- | --- |
| Prefix-list | Sélectionner préfixes et longueurs |
| Route-map / policy | Appliquer des conditions et actions |
| Route tag | Marquer une origine ou une politique de réinjection |
| Summary/default | Réduire la quantité de routes exposées selon le besoin |

Une redistribution bidirectionnelle à plusieurs points peut réintroduire une route dans son domaine d'origine. Les préférences administratives, chemins de retour et conditions de panne peuvent alors produire des boucles ou chemins incohérents. Les tags aident à filtrer les réinjections mais ne constituent pas une protection magique sans politique correctement appliquée.

Le filtrage peut agir à des endroits différents selon le protocole. Bloquer une route dans la RIB locale n'équivaut pas nécessairement à retirer une information de LSDB ou à empêcher une annonce distante.

La validation doit couvrir le régime normal et une panne d'un point de redistribution. Les routes de synthèse peuvent attirer du trafic pour des sous-réseaux absents.

## Exemple concret

Deux routeurs relient OSPF et EIGRP. Un préfixe OSPF est injecté dans EIGRP puis réinjecté dans OSPF par l'autre routeur. Une politique de tags et de filtrage doit identifier ce retour et le refuser selon le design.

## Pièges à éviter

- Redistribuer toutes les routes sans liste explicite.
- Transposer une métrique numérique entre protocoles.
- Tester uniquement la topologie sans panne.

## Ce qu’il faut observer

Tracer origine, marquage, métrique, type externe et point de réinjection du même préfixe. Comparer les chemins après perte d’un redistributeur.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

Pourquoi définir une seed metric ?

<details><summary>Afficher la correction</summary>

Le protocole cible a besoin d’une métrique dans son propre système.

</details>

### Question 2

Un tag empêche-t-il une boucle à lui seul ?

<details><summary>Afficher la correction</summary>

Non. Une politique doit l’exploiter aux points appropriés.

</details>

### Question 3

Pourquoi examiner les résumés ?

<details><summary>Afficher la correction</summary>

Ils peuvent annoncer une couverture plus large que les routes effectivement disponibles.

</details>

## Sources pour approfondir

- [RFC 2328](https://www.rfc-editor.org/rfc/rfc2328)
- [RFC 7868](https://www.rfc-editor.org/rfc/rfc7868)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
