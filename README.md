# Network Revision Companion

**Ton compagnon de révision réseau, en français.**

40 fiches expliquent les bases des couches 1 à 4, les protocoles de routage et les architectures qui les assemblent. Chaque fiche contient un mécanisme expliqué, un exemple, des pièges, des points d’observation et trois questions avec corrections masquées.

`40 fiches` · `123 questions corrigées` · `8 domaines` · `Références primaires`

## Choisir comment réviser

| Besoin | Point d’entrée |
| --- | --- |
| Reprendre progressivement | [Parcours de révision](revision/parcours.md) |
| Distinguer deux notions proches | [Tableaux comparatifs](revision/comparaisons.md) |
| Retrouver un protocole ou un port | [Repères de transport](revision/protocoles-et-ports.md) |
| Décoder un terme | [Glossaire](revision/glossaire.md) |
| Expliquer un chemin complet | [Cas de synthèse](revision/cas-de-synthese.md) |
| Suivre sa progression | [Checklist des 40 fiches](revision/progression.md) |

## Sommaire des fiches

### Fondations et couche physique

| Fiche | Sujet |
| --- | --- |
| 01 | [OSI, encapsulation et chemin d’un paquet](fiches/01-fondations/01-osi-et-chemin-du-paquet.md) |
| 02 | [Cuivre, fibre, optiques et PoE](fiches/01-fondations/02-cuivre-fibre-optique-poe.md) |

### Ethernet et switching L2

| Fiche | Sujet |
| --- | --- |
| 03 | [Ethernet, apprentissage MAC et flooding](fiches/02-switching/03-ethernet-mac.md) |
| 04 | [VLAN, trunk 802.1Q et QinQ](fiches/02-switching/04-vlan-trunk-qinq.md) |
| 05 | [STP et choix du chemin sans boucle](fiches/02-switching/05-stp.md) |
| 06 | [RSTP et MSTP](fiches/02-switching/06-rstp-mstp.md) |
| 07 | [PVST+, Rapid PVST+ et interopérabilité](fiches/02-switching/07-pvst-rapid-pvst.md) |
| 08 | [LACP, port-channel et MLAG](fiches/02-switching/08-lacp-mlag.md) |
| 09 | [LLDP, découverte et cartographie](fiches/02-switching/09-lldp-et-decouverte.md) |

### IP, routage et convergence

| Fiche | Sujet |
| --- | --- |
| 10 | [IPv4, CIDR, VLSM et calcul de sous-réseaux](fiches/03-ip-et-routage/10-ipv4-et-subnetting.md) |
| 11 | [IPv6, adressage et découverte de routeur](fiches/03-ip-et-routage/11-ipv6.md) |
| 12 | [ARP, Neighbor Discovery et ICMP](fiches/03-ip-et-routage/12-arp-nd-icmp.md) |
| 13 | [RIB, FIB et choix de route](fiches/03-ip-et-routage/13-rib-fib-et-selection.md) |
| 14 | [OSPF, adjacencies, zones et LSA](fiches/03-ip-et-routage/14-ospf.md) |
| 15 | [EIGRP, DUAL et condition de faisabilité](fiches/03-ip-et-routage/15-eigrp.md) |
| 16 | [IS-IS, niveaux et TLV](fiches/03-ip-et-routage/16-isis.md) |
| 17 | [BGP, attributs et politique de chemin](fiches/03-ip-et-routage/17-bgp.md) |
| 18 | [MP-BGP, AFI/SAFI et familles de routes](fiches/03-ip-et-routage/18-mp-bgp.md) |
| 19 | [Redistribution, filtrage et prévention des boucles](fiches/03-ip-et-routage/19-redistribution-filtrage.md) |
| 20 | [VRF, VRF-Lite et route leaking](fiches/03-ip-et-routage/20-vrf.md) |
| 39 | [Multicast, IGMP, MLD et PIM](fiches/03-ip-et-routage/39-multicast.md) |
| 40 | [HSRP, VRRP, BFD et convergence](fiches/03-ip-et-routage/40-resilience-fhrp-bfd.md) |

### MPLS, VPN et overlays

| Fiche | Sujet |
| --- | --- |
| 21 | [MPLS, labels et transport](fiches/04-mpls-et-overlays/21-mpls.md) |
| 22 | [MPLS L3VPN, RD, RT et MP-BGP](fiches/04-mpls-et-overlays/22-mpls-l3vpn.md) |
| 23 | [L2VPN, pseudowire, VPWS et VPLS](fiches/04-mpls-et-overlays/23-l2vpn.md) |
| 24 | [VXLAN, VTEP, VNI et underlay](fiches/04-mpls-et-overlays/24-vxlan.md) |
| 25 | [EVPN, routes BGP et IRB](fiches/04-mpls-et-overlays/25-evpn.md) |

### Transport et services IP

| Fiche | Sujet |
| --- | --- |
| 26 | [TCP, fiabilité, fenêtres et congestion](fiches/05-transport-et-services/26-tcp.md) |
| 27 | [UDP et responsabilité de l’application](fiches/05-transport-et-services/27-udp.md) |
| 28 | [MTU, MSS, fragmentation et PMTUD](fiches/05-transport-et-services/28-mtu-mss-pmtud.md) |
| 29 | [DHCP, DNS et NTP comme dépendances réseau](fiches/05-transport-et-services/29-dhcp-dns-ntp.md) |
| 30 | [NAT, PAT et lecture d’un flux traduit](fiches/05-transport-et-services/30-nat-pat.md) |
| 31 | [QoS, DSCP, files, policing et shaping](fiches/05-transport-et-services/31-qos.md) |

### Sécurité et WAN

| Fiche | Sujet |
| --- | --- |
| 32 | [ACL, firewall stateful et IPsec](fiches/06-securite-et-sdwan/32-acl-firewall-ipsec.md) |
| 33 | [SD-WAN, underlay, overlay et politique applicative](fiches/06-securite-et-sdwan/33-sdwan.md) |

### Contrôle d’accès et Wi-Fi

| Fiche | Sujet |
| --- | --- |
| 34 | [NAC, 802.1X, EAP, RADIUS et CoA](fiches/07-acces-et-wifi/34-nac.md) |
| 35 | [Wi-Fi, radio, canaux et airtime](fiches/07-acces-et-wifi/35-wifi-radio.md) |
| 36 | [Wi-Fi, association, sécurité et roaming](fiches/07-acces-et-wifi/36-wifi-securite-roaming.md) |

### Observation et diagnostic

| Fiche | Sujet |
| --- | --- |
| 37 | [SNMP, télémétrie, logs et données de flux](fiches/08-exploitation/37-observabilite.md) |
| 38 | [Dépanner de L1 à L4 avec un flux témoin](fiches/08-exploitation/38-diagnostic-transversal.md) |

## Relier théorie et pratique

Après une fiche, explique le mécanisme sans la relire, réponds aux trois questions puis vérifie tes réponses. Termine par une observation ou un mini-lab sur ton matériel de test.

Les dépôts [network-engineering-labs](https://github.com/netpython/network-engineering-labs) et [network-troubleshooting-labs](https://github.com/netpython/network-troubleshooting-labs) complètent ce compagnon avec des objectifs pratiques et des incidents. Les [cheat sheets CLI](https://github.com/netpython/network-cli-cheatsheets) servent à retrouver la syntaxe des commandes.

## Portée et sources

Les couches OSI donnent la base. DHCP, DNS, NTP, NAC et SD-WAN sont aussi abordés comme services ou architectures transverses, pour comprendre leurs dépendances L1–L4.

Les fiches sont des synthèses pédagogiques originales. Elles renvoient aux RFC, aux groupes IEEE et à des documentations constructeur pour les mécanismes propres à un produit. Une fonction décrite conceptuellement ne garantit pas sa disponibilité sur un modèle ou une version. Les liens internes et calculs d’exemple ont été contrôlés. La collecte de commandes et les essais matériels restent du ressort des labs.

Commence par la [fiche OSI et chemin du paquet](fiches/01-fondations/01-osi-et-chemin-du-paquet.md) ou ouvre directement le thème à rafraîchir.

## Approfondissements

- [Renouvellement DHCPv4 : T1, T2 et expiration du bail](fiches/05-transport-et-services/29-dhcp-dns-ntp.md#approfondissement--renouvellement-dhcpv4) — cas horaire et questions complémentaires.
