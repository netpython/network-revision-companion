# 07 · PVST+, Rapid PVST+ et interopérabilité

[Fiche précédente](../02-switching/06-rstp-mstp.md) · [Sommaire](../../README.md) · [Fiche suivante](../02-switching/08-lacp-mlag.md)

## Comprendre

PVST+ et Rapid PVST+ sont des implémentations Cisco maintenant une instance de spanning tree par VLAN. PVST+ s'appuie sur le comportement STP classique, Rapid PVST+ sur le comportement rapide.

| Mode | Unité de topologie | Point d'attention |
| --- | --- | --- |
| STP/RSTP commun | Domaine ou instance commune | Topologie partagée |
| PVST+ / Rapid PVST+ | VLAN | Nombre d'instances et placement des racines |
| MSTP | Groupes de VLANs par instance | Cohérence de région et frontières |

L'identifiant système étendu intègre le VLAN à l'affichage du Bridge ID sur les équipements concernés. Une priorité configurée de 4096 dans le VLAN 20 peut donc être affichée comme 4116 dans le Bridge ID. Il faut distinguer la valeur configurée et la valeur affichée.

Avoir une racine différente selon le VLAN peut répartir les chemins, mais un alignement avec la passerelle active évite des traversées inutiles. Ce choix dépend aussi des architectures MLAG ou de routage au plus près des hôtes.

L'interopérabilité avec MSTP ou un spanning tree commun requiert une lecture des mécanismes de frontière. Une configuration cohérente d'un seul VLAN ne prouve pas la cohérence du campus entier.

## Exemple concret

Le root du VLAN 10 se trouve sur D1 alors que sa passerelle active est sur D2. Cela peut ajouter une traversée du lien de distribution. L'alignement racine/passerelle mérite d'être examiné à partir du chemin réel.

## Pièges à éviter

- Confondre Rapid PVST+ avec une norme IEEE universelle.
- Lire seulement l’instance du VLAN 1.
- Interpréter l’ID système étendu comme une modification inexpliquée de priorité.

## Ce qu’il faut observer

Examiner root et rôles par VLAN, priorités, état des trunks et comportement aux frontières MST/PVST.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

Rapid PVST+ maintient-il une instance unique pour tout le switch ?

<details><summary>Afficher la correction</summary>

Non. Il maintient une instance par VLAN pris en charge.

</details>

### Question 2

Pourquoi une priorité 4096 apparaît-elle à 4116 pour VLAN 20 ?

<details><summary>Afficher la correction</summary>

L’affichage intègre l’identifiant système étendu du VLAN.

</details>

### Question 3

Pourquoi comparer racine STP et passerelle active ?

<details><summary>Afficher la correction</summary>

Leur placement influence le trajet L2 avant le routage.

</details>

## Sources pour approfondir

- [Documentation de référence 1](https://www.cisco.com/c/en/us/td/docs/switches/lan/c9000/lyr2-fwd/stp/stp-configuration-guide/m-stp.html)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
