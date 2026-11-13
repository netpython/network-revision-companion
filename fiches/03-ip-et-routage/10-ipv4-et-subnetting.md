# 10 · IPv4, CIDR, VLSM et calcul de sous-réseaux

[Fiche précédente](../02-switching/09-lldp-et-decouverte.md) · [Sommaire](../../README.md) · [Fiche suivante](../03-ip-et-routage/11-ipv6.md)

## Comprendre

Un préfixe IPv4 /n fixe les n bits du réseau. Les bits restants définissent les adresses du bloc. CIDR permet des tailles variables, et VLSM consiste à attribuer des blocs de tailles différentes selon les besoins.

| Préfixe | Adresses dans le bloc | Hôtes usuels sur un LAN classique |
| --- | ---: | ---: |
| /24 | 256 | 254 |
| /25 | 128 | 126 |
| /26 | 64 | 62 |
| /30 | 4 | 2 |
| /31 | 2 | Usage point à point selon support |
| /32 | 1 | Route hôte ou loopback |

Sur un LAN IPv4 classique, l'adresse réseau et le broadcast ne sont pas attribués à des hôtes. Le /31 point à point est une exception normalisée. Le /32 représente une seule adresse.

Une route résumée doit être alignée sur une frontière binaire et peut inclure des réseaux non effectivement utilisés. Il faut considérer les trous du résumé et les routes de rejet éventuelles. Une réserve d'adresses n'est pas interchangeable avec une réserve de ports ou de débit.

Le masque intervient dans la décision locale d'envoyer directement au voisin ou à la passerelle. Des masques incohérents peuvent créer des visions asymétriques du même réseau.

## Exemple concret

192.0.2.64/26 couvre 192.0.2.64 à 192.0.2.127. Les adresses hôtes usuelles vont de .65 à .126. L'adresse .130 appartient au bloc /26 suivant, qui débute à .128.

## Pièges à éviter

- Soustraire systématiquement deux adresses pour tous les préfixes.
- Créer un résumé non aligné.
- Dimensionner sans réserve ni contrainte d’agrégation.

## Ce qu’il faut observer

Calculer réseau, bornes, broadcast et plage utilisable. Vérifier les chevauchements dans une même table de routage et comparer les masques des voisins.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

Combien d’adresses contient un /23 ?

<details><summary>Afficher la correction</summary>

512 adresses, soit 510 hôtes usuels sur un LAN classique.

</details>

### Question 2

Un /31 est-il toujours inutilisable ?

<details><summary>Afficher la correction</summary>

Non. Il est prévu pour des liens point à point lorsque les équipements le prennent en charge.

</details>

### Question 3

192.0.2.64/26 contient-il .127 ?

<details><summary>Afficher la correction</summary>

Oui comme adresse de broadcast du bloc, pas comme adresse hôte usuelle.

</details>

## Sources pour approfondir

- [RFC 4632](https://www.rfc-editor.org/rfc/rfc4632)
- [RFC 3021](https://www.rfc-editor.org/rfc/rfc3021)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
