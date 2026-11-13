# 06 · RSTP et MSTP

[Fiche précédente](../02-switching/05-stp.md) · [Sommaire](../../README.md) · [Fiche suivante](../02-switching/07-pvst-rapid-pvst.md)

## Comprendre

RSTP améliore la convergence en utilisant des rôles et des échanges plus explicites. Les rôles root, designated, alternate et backup décrivent la position d'un port. Les états sont regroupés en discarding, learning et forwarding.

Une transition rapide repose notamment sur les liens point à point, le mécanisme proposal/agreement et le comportement edge. Elle dépend de la topologie et de la compatibilité des voisins. Dire qu'elle est toujours instantanée masque les conditions nécessaires.

MSTP associe plusieurs VLANs à un nombre limité d'instances de spanning tree. Une région MST est identifiée par des paramètres cohérents de nom, révision et mapping VLAN/instance. Le numéro de révision fait partie de l'identité et ne constitue pas un mécanisme qui impose automatiquement une configuration aux voisins.

| Élément | Fonction |
| --- | --- |
| CIST | Vue commune reliant les régions et domaines externes |
| IST | Instance interne de référence dans la région |
| MSTI | Instance supplémentaire portant un groupe de VLANs |

Les frontières de région influencent les chemins et l'interopérabilité. Regrouper des VLANs réduit le nombre d'instances, mais impose de réfléchir à leur placement commun. La même région doit être vérifiée sur l'ensemble des switches concernés.

## Exemple concret

Les VLANs 10 et 20 sont mappés à MSTI 1, les VLANs 30 et 40 à MSTI 2. Deux switches avec un mapping différent ne partagent pas la même identité de région, même si leur nom semble identique.

## Pièges à éviter

- Assimiler une révision MST supérieure à une priorité de configuration.
- Attendre une convergence identique sur des liens ou voisins différents.
- Changer un mapping sans évaluer les frontières de région.

## Ce qu’il faut observer

Comparer le digest ou les paramètres de région, les instances, les rôles des ports et la relation avec les domaines voisins.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

Pourquoi RSTP est-il plus rapide dans des conditions favorables ?

<details><summary>Afficher la correction</summary>

Il utilise des mécanismes explicites de transition et des rôles de secours, au lieu de dépendre seulement des délais STP classiques.

</details>

### Question 2

Une révision MST élevée pousse-t-elle le mapping aux voisins ?

<details><summary>Afficher la correction</summary>

Non. Elle participe à l’identité de région.

</details>

### Question 3

Deux VLANs dans la même MSTI peuvent-ils choisir chacun une racine indépendante ?

<details><summary>Afficher la correction</summary>

Ils partagent la topologie de cette instance au sein de la région.

</details>

## Sources pour approfondir

- [Documentation de référence 1](https://www.ieee802.org/1/pages/802.1Q.html)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
