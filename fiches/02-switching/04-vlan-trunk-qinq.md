# 04 · VLAN, trunk 802.1Q et QinQ

[Fiche précédente](../02-switching/03-ethernet-mac.md) · [Sommaire](../../README.md) · [Fiche suivante](../02-switching/05-stp.md)

## Comprendre

Un VLAN sépare des domaines de broadcast sur une infrastructure de commutation commune. Un port access transporte usuellement le trafic d'un VLAN vers un terminal non tagué. Un trunk transporte plusieurs VLANs avec une identification 802.1Q.

| Terme | Rôle |
| --- | --- |
| VLAN ID | Identifie le VLAN dans le contexte L2 |
| PVID / native VLAN | Classe le trafic non tagué selon la configuration du port |
| Allowed list | Définit les VLANs admissibles sur le trunk |
| QinQ | Ajoute un tag de service autour d'un tag client |

Le champ VID fait 12 bits. Les valeurs 0 et 4095 ont un traitement particulier et les VLANs usuels vont de 1 à 4094, sous réserve des limitations produit. L'usage du VLAN natif et le tagging des trames natives dépendent du paramétrage et du constructeur.

Une allowed list ne crée pas le VLAN et ne prouve pas qu'il est en forwarding. Il faut vérifier existence, membership et état STP. Un mauvais classement des trames non taguées peut connecter deux domaines inattendus.

QinQ permet de transporter un service client à travers un domaine opérateur avec un tag supplémentaire. Il faut dimensionner la taille des trames et comprendre les points d'ajout/retrait des tags. Un VLAN n'assure pas à lui seul un contrôle de sécurité équivalent à une politique de filtrage.

## Exemple concret

VLAN 20 existe sur deux switches. Le trunk n'autorise que 10 et 30. Les ports peuvent être up et le VLAN créé localement, mais les hôtes du VLAN 20 ne traversent pas ce trunk.

## Pièges à éviter

- Confondre VLAN créé et VLAN autorisé sur un lien.
- Remplacer une allowed list alors qu’un ajout ciblé suffit.
- Supposer qu’une native VLAN est toujours taguée ou toujours non taguée.

## Ce qu’il faut observer

Comparer mode access/trunk, tags observés, PVID/native VLAN, VLANs autorisés et état de forwarding aux deux extrémités.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

Une allowed list crée-t-elle le VLAN ?

<details><summary>Afficher la correction</summary>

Non. Création du VLAN et transport sur le port sont des états distincts.

</details>

### Question 2

Combien d’octets ajoute un tag 802.1Q ?

<details><summary>Afficher la correction</summary>

Quatre octets.

</details>

### Question 3

Pourquoi QinQ influence-t-il la taille maximale des trames ?

<details><summary>Afficher la correction</summary>

Le tag extérieur ajoute de l’overhead en plus du tag client éventuel.

</details>

## Sources pour approfondir

- [Documentation de référence 1](https://www.ieee802.org/1/pages/802.1Q.html)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
