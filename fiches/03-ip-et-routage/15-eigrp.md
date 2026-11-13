# 15 · EIGRP, DUAL et condition de faisabilité

[Fiche précédente](../03-ip-et-routage/14-ospf.md) · [Sommaire](../../README.md) · [Fiche suivante](../03-ip-et-routage/16-isis.md)

## Comprendre

EIGRP est un IGP fondé sur un algorithme de type distance-vector avancé, DUAL. Il construit des voisinages et une table topologique. Le successor représente le chemin choisi. Un feasible successor satisfait une condition permettant de le considérer comme un secours sans boucle.

La reported distance est la distance annoncée par le voisin vers la destination. La feasible distance est une valeur de référence de DUAL dont l'historique importe. La condition de faisabilité compare la reported distance du candidat à cette feasible distance avec une inégalité stricte.

| Terme | Sens |
| --- | --- |
| Successor | Chemin sélectionné |
| Feasible successor | Candidat répondant à la condition de faisabilité |
| Passive | Route stable, hors calcul diffusant |
| Active | Recherche ou recalcul diffusant pour la route |

Active ne signifie pas « route utilisée ». En l'absence de secours faisable, le protocole peut interroger les voisins. Un domaine de queries mal borné peut amplifier la convergence. Le mode stub réduit certains échanges et doit correspondre au rôle du site.

La métrique composite dépend des K-values et de l'implémentation. Les valeurs classiques par défaut utilisent principalement bande passante minimale du chemin et délai cumulé. Les K-values doivent être compatibles pour le voisinage. La RFC 7868 décrit EIGRP à titre informatif, sans transformer toutes ses implémentations en standard IETF universel.

## Exemple concret

Une reported distance de 80 satisfait une feasible distance de référence de 100. Une reported distance de 100 ne satisfait pas la condition stricte. La métrique totale via ce voisin sert ensuite au classement du chemin.

## Pièges à éviter

- Assimiler l’état Active à une route opérationnelle.
- Utiliser une inégalité large au lieu de stricte.
- Supposer que toutes les K-values ont les mêmes réglages sur tous les voisins.

## Ce qu’il faut observer

Relever voisins, FD/RD, successors, état de route et portée des queries. Vérifier K-values, stub et taille du domaine de panne.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

RD=FD satisfait-il la faisabilité ?

<details><summary>Afficher la correction</summary>

Non. La reported distance doit être strictement inférieure à la feasible distance de référence.

</details>

### Question 2

Pourquoi un chemin physiquement disponible peut-il ne pas être feasible successor ?

<details><summary>Afficher la correction</summary>

Sa distance annoncée ne satisfait pas nécessairement la condition de faisabilité.

</details>

### Question 3

À quoi sert le stub ?

<details><summary>Afficher la correction</summary>

À limiter certains échanges et la portée des queries pour un rôle de bord de réseau adapté.

</details>

## Sources pour approfondir

- [RFC 7868](https://www.rfc-editor.org/rfc/rfc7868)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
