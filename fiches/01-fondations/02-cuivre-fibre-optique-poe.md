# 02 · Cuivre, fibre, optiques et PoE

[Fiche précédente](../01-fondations/01-osi-et-chemin-du-paquet.md) · [Sommaire](../../README.md) · [Fiche suivante](../02-switching/03-ethernet-mac.md)

## Comprendre

La couche physique transforme les bits en signaux. La capacité dépend du standard Ethernet, du média, de la longueur, des connecteurs et des caractéristiques des émetteurs. Une liaison optique exige un couple compatible de débit, longueur d'onde, fibre et budget optique.

| Élément | Ce qu'il faut comparer |
| --- | --- |
| Cuivre | Catégorie, longueur, paires, certification et environnement |
| Multimode / monomode | Fibre attendue par l'optique et distance supportée |
| SFP / SFP+ / QSFP | Format mécanique et compatibilité électrique/logicielle |
| DOM | Puissance reçue/émise et seuils propres à l'optique |
| PoE | Standard, classe du terminal, budget du port et budget global |

La marge optique se raisonne en puissance. La différence entre puissance d'émission et sensibilité du récepteur doit absorber les pertes et une marge. Une puissance reçue excessive peut également dépasser la plage du récepteur. dBm exprime une puissance absolue, dB un rapport.

Le full-duplex sépare les émissions des deux extrémités. La collision caractérise le partage half-duplex historique. Une négociation ou un média défaillant peut produire un lien actif accompagné d'erreurs. Le PoE fournit l'énergie au terminal et consomme une réserve globale dépendant des alimentations et des modes de redondance.

## Exemple concret

Une optique émet à -3 dBm et le récepteur accepte jusqu'à -12 dBm de sensibilité minimale. La marge théorique avant réserve est 9 dB. Avec 6 dB de pertes estimées, il reste 3 dB. Cet exemple simplifié doit être complété par les limites réelles du couple d'optiques.

## Pièges à éviter

- Assimiler un format SFP à un débit ou une portée garantis.
- Comparer les puissances optiques à un seuil universel.
- Dimensionner le PoE uniquement avec le nombre de ports.

## Ce qu’il faut observer

Comparer débit, duplex, erreurs croissantes, pertes de lien, référence des optiques, valeurs DOM, budget PoE et effet d’une alimentation perdue.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

Quelle différence entre dB et dBm ?

<details><summary>Afficher la correction</summary>

dB exprime un rapport, dBm une puissance référencée à 1 mW.

</details>

### Question 2

Un lien up prouve-t-il un média sain ?

<details><summary>Afficher la correction</summary>

Non. Il faut aussi examiner les erreurs et la stabilité sous trafic.

</details>

### Question 3

Pourquoi vérifier le PoE en mode dégradé ?

<details><summary>Afficher la correction</summary>

La perte d’une alimentation peut réduire la puissance disponible et entraîner la coupure de terminaux.

</details>

## Sources pour approfondir

- [Documentation de référence 1](https://www.ieee802.org/3/)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
