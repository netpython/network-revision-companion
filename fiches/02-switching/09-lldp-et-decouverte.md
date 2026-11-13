# 09 · LLDP, découverte et cartographie

[Fiche précédente](../02-switching/08-lacp-mlag.md) · [Sommaire](../../README.md) · [Fiche suivante](../03-ip-et-routage/10-ipv4-et-subnetting.md)

## Comprendre

LLDP est un protocole de découverte de voisins directement connectés. Il transporte des informations sous forme de TLV, notamment identifiants de châssis et de port. LLDP-MED ajoute des usages utiles à certains terminaux, comme des politiques de réseau voix.

CDP est une technologie Cisco poursuivant un objectif proche. La présence de l'un ou l'autre dépend de l'activation, du support et des politiques de l'environnement.

| Information | Utilité | Limite |
| --- | --- | --- |
| Chassis ID | Identifier le voisin | Format variable |
| Port ID | Retrouver le lien distant | Peut être MAC ou nom |
| Management address | Localiser une adresse annoncée | Ne prouve pas sa joignabilité |
| Capabilities | Décrire des rôles | Dépend de l'annonce |

La découverte sert à reconstituer le câblage, détecter un branchement inattendu et comparer l'inventaire à l'état observé. Elle reste locale au lien. Une entrée vieillie ou une fonction désactivée peut expliquer l'absence de voisin.

L'information annoncée doit être corroborée par la configuration et, si nécessaire, le câblage. Exposer nom, modèle et adresse de gestion sur un port non maîtrisé peut révéler des informations d'infrastructure. Le choix d'activation doit refléter le rôle du port.

## Exemple concret

Un switch annonce son port sous forme de MAC plutôt que de nom d'interface. La cartographie doit conserver Chassis ID et Port ID au lieu de traiter un System Name vide comme un voisin absent.

## Pièges à éviter

- Confondre absence de voisin LLDP et absence de lien.
- Supposer que l’adresse de gestion annoncée est accessible depuis le poste d’administration.
- Identifier un équipement uniquement par un nom non unique.

## Ce qu’il faut observer

Comparer identifiant de châssis, port local, port distant, âge/TTL et capacités. Rechercher les incohérences avec le câblage prévu.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

LLDP décrit-il un voisin à plusieurs sauts ?

<details><summary>Afficher la correction</summary>

Il décrit normalement un voisin directement connecté sur le lien.

</details>

### Question 2

Pourquoi conserver plusieurs identifiants ?

<details><summary>Afficher la correction</summary>

Un nom peut manquer ou être dupliqué, tandis que Chassis ID et Port ID précisent la relation observée.

</details>

### Question 3

Une adresse annoncée est-elle un test de connectivité ?

<details><summary>Afficher la correction</summary>

Non. Une annonce et la joignabilité sont des preuves différentes.

</details>

## Sources pour approfondir

- [Documentation de référence 1](https://www.ieee802.org/1/pages/802.1AB.html)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
