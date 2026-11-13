# 03 · Ethernet, apprentissage MAC et flooding

[Fiche précédente](../01-fondations/02-cuivre-fibre-optique-poe.md) · [Sommaire](../../README.md) · [Fiche suivante](../02-switching/04-vlan-trunk-qinq.md)

## Comprendre

Un switch apprend une association entre MAC source, VLAN et port d'entrée à partir des trames reçues. La table de commutation permet ensuite de choisir le port de sortie d'une MAC destination connue.

| Destination | Comportement usuel dans le VLAN |
| --- | --- |
| Unicast connue | Envoi vers le port associé |
| Unicast inconnue | Flooding vers les ports admissibles hors port d'entrée |
| Broadcast | Diffusion dans le domaine de broadcast |
| Multicast | Dépend du groupe, du snooping et de la plateforme |

L'âge des entrées limite la conservation d'informations devenues obsolètes. Une MAC mobile peut être légitime, mais des mouvements répétés peuvent révéler une boucle ou une incohérence d'agrégation. Le FCS détecte des erreurs de trame. Un FCS correct ne garantit pas que le paquet ou l'application est valide.

Une trame Ethernet usuelle comporte les MAC destination/source, le champ type/longueur, la charge et le FCS. Un tag 802.1Q ajoute quatre octets. Le préambule et l'intervalle entre trames comptent pour le débit sur le fil, mais ne sont pas inclus de la même façon dans toutes les tailles de trame annoncées.

Un domaine de broadcast est généralement délimité par un VLAN. Le routage permet de communiquer entre domaines, selon les politiques appliquées.

## Exemple concret

PC-A envoie pour la première fois à PC-B dans le même VLAN. Si la MAC de B est inconnue, le switch diffuse la trame. La réponse de B permet l'apprentissage de sa MAC source et les échanges suivants utilisent le port connu.

## Pièges à éviter

- Dire que le switch apprend la MAC destination en lisant une trame.
- Interpréter toute unicast inconnue comme une attaque.
- Comparer des compteurs de taille sans connaître ce qui inclut le FCS ou les tags.

## Ce qu’il faut observer

Comparer VLAN, MAC source, port d’entrée, port appris et évolution de la table. Examiner les mouvements MAC et les erreurs physiques.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

Quelle MAC sert à l’apprentissage ?

<details><summary>Afficher la correction</summary>

La MAC source de la trame reçue.

</details>

### Question 2

Une unicast inconnue traverse-t-elle tous les VLANs ?

<details><summary>Afficher la correction</summary>

Non. Le flooding reste dans le domaine L2 concerné et respecte les états et politiques des ports.

</details>

### Question 3

Pourquoi une MAC peut-elle disparaître de la table ?

<details><summary>Afficher la correction</summary>

Vieillissement, événement de topologie, remise à zéro ou déplacement peuvent modifier l’entrée.

</details>

## Sources pour approfondir

- [Documentation de référence 1](https://www.ieee802.org/1/pages/802.1Q.html)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
