# 35 · Wi-Fi, radio, canaux et airtime

[Fiche précédente](../07-acces-et-wifi/34-nac.md) · [Sommaire](../../README.md) · [Fiche suivante](../07-acces-et-wifi/36-wifi-securite-roaming.md)

## Comprendre

Le Wi-Fi partage un média radio. Le débit de lien indiqué est un débit physique, distinct du débit applicatif. L'accès au canal, les acquittements, les retransmissions et les autres stations consomment du temps d'antenne.

| Mesure | Sens |
| --- | --- |
| RSSI | Indication de puissance reçue, selon mesure et outil |
| SNR | Rapport entre signal et bruit |
| Utilisation du canal | Part du temps observée comme occupée |
| Retries | Répétitions pouvant refléter des problèmes de réception ou de contention |
| MCS | Combinaison de modulation et de codage, avec d'autres paramètres PHY |

Augmenter la largeur de canal peut augmenter le débit PHY, mais réduit les possibilités de réutilisation et peut accroître la concurrence. Le choix dépend de la densité, des clients et des règles radio locales. La disponibilité des bandes, canaux et puissances doit être vérifiée selon le pays.

Le canal est partagé. Un client lent ou éloigné peut consommer beaucoup d'airtime. Des stations cachées peuvent mal détecter leurs émissions mutuelles. Plus d'AP ou plus de puissance n'améliorent pas mécaniquement la capacité.

MIMO, OFDMA et les mécanismes multi-utilisateurs améliorent certains usages sous conditions de support et de planification. Le nombre de flux spatiaux utilisable dépend aussi du terminal.

## Exemple concret

Deux AP proches utilisent le même canal. Les clients affichent un signal fort, mais leur débit baisse aux heures de pointe. Il faut examiner l'occupation et la contention plutôt que d'augmenter encore la puissance.

## Pièges à éviter

- Assimiler un RSSI élevé à une capacité suffisante.
- Comparer un débit PHY avec un débit TCP utile.
- Réutiliser un plan de canaux sans vérifier la réglementation et la densité.

## Ce qu’il faut observer

Mesurer radio depuis le client et l’AP, occupation, bruit, retries, largeur de canal, MCS et densité. Relier ces mesures au service.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

Pourquoi le débit applicatif est-il inférieur au PHY ?

<details><summary>Afficher la correction</summary>

Le média et les protocoles consomment du temps et de l’overhead, auquel s’ajoutent les conditions radio et les reprises.

</details>

### Question 2

Un canal plus large est-il toujours préférable ?

<details><summary>Afficher la correction</summary>

Non. Il réduit la réutilisation et peut aggraver la concurrence.

</details>

### Question 3

Pourquoi mesurer depuis le terminal ?

<details><summary>Afficher la correction</summary>

La réception et les capacités du client peuvent différer fortement de la vue de l’AP.

</details>

## Sources pour approfondir

- [Documentation de référence 1](https://www.ieee802.org/11/)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
