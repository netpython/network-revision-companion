# Les distinctions qui évitent les erreurs

## VLAN, VRF, VNI, RD et RT

| Notion | Fonction | À vérifier |
| --- | --- | --- |
| VLAN | Domaine de commutation local | Ports et tags |
| VRF | Contexte de routage | Interfaces et tables |
| VNI | Segment de l’overlay VXLAN | Mapping de service |
| RD | Différenciation des préfixes VPN | Identité de route |
| RT | Politique d’import/export | Appartenance du service |

## STP, RSTP, PVST et MSTP

| Famille | Repère | Limite de la simplification |
| --- | --- | --- |
| STP classique | Élections et transitions avec états intermédiaires | La topologie et les timers influencent la convergence |
| RSTP | Rôles et procédures rapides | Rapidité conditionnée au contexte |
| PVST+ | Une instance par VLAN, comportement classique | Implémentation Cisco |
| Rapid PVST+ | Une instance par VLAN, comportement rapide | Interopérabilité à contrôler |
| MSTP | Plusieurs VLANs associés à des instances | Identité de région et frontières |

## OSPF, IS-IS, EIGRP et BGP

| Protocole | Approche | Domaine courant | Transport de contrôle |
| --- | --- | --- | --- |
| OSPF | État de liens, SPF | IGP | Directement IP, numéro 89 |
| IS-IS | État de liens, SPF | IGP | Directement sur la liaison |
| EIGRP | DUAL, distance-vector avancé | IGP | Directement IP, numéro 88 |
| BGP | Échange de chemins et politique | Inter-AS et contrôle interne | TCP 179 |

Le choix d’un protocole ne se réduit pas à sa métrique. Les règles de propagation, le domaine d’échec et la politique comptent aussi.

## RIB, FIB et bases de protocole

| Table | Contenu principal |
| --- | --- |
| Base OSPF / topologie EIGRP / table BGP | Informations propres au protocole |
| RIB | Routes retenues selon les mécanismes du système |
| FIB | Informations utilisées pour le forwarding |
| Adjacencies / voisins | Résolution locale vers le prochain saut |

## TCP et UDP

| Aspect | TCP | UDP |
| --- | --- | --- |
| Unité de service | Flux d’octets | Datagrammes |
| Établissement de transport | État et handshake | Aucun handshake UDP |
| Fiabilité | Fournie par TCP | Peut être ajoutée par l’application |
| Congestion | Contrôle TCP | Responsabilité du protocole/applicatif concerné |
| Frontières de messages | À gérer par l’application | Frontières de datagrammes conservées |

## Policing et shaping

| Mécanisme | Traitement de l’excédent |
| --- | --- |
| Policing | Drop ou remark selon profil/politique |
| Shaping | Mise en attente et lissage dans les limites de buffer |

## MPLS et VXLAN, puis VPN et EVPN

| Élément | Fonction |
| --- | --- |
| MPLS | Forwarding à labels |
| VXLAN | Encapsulation Ethernet sur UDP/IP |
| MPLS L3VPN | Service L3 séparé par VRF et distribué via BGP |
| EVPN | Contrôle BGP de services Ethernet/overlay |

EVPN peut accompagner différents transports. Les noms de service, contrôle et encapsulation désignent des responsabilités distinctes.

## Authentification et autorisation

| Étape | Question |
| --- | --- |
| Authentification | Quelle identité et quelle preuve sont reconnues ? |
| Autorisation | Quels accès et rôles sont accordés à cette session ? |
| Accounting | Quelles traces de session sont enregistrées ? |

## Haute disponibilité et convergence

| Notion | Question |
| --- | --- |
| Redondance | Quel composant peut remplacer celui qui échoue ? |
| Détection | Quel événement révèle la panne ? |
| Convergence | Quand les décisions et états deviennent-ils cohérents ? |
| Restauration de service | Quand l’utilisateur réussit-il son opération ? |

Ces tableaux sont des repères. Les mécanismes et sources détaillés sont accessibles dans les [40 fiches](../README.md).
