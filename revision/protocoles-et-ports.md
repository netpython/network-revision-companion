# Repères de transport et identifiants

Un numéro de protocole IP n’est pas un port TCP/UDP. Un EtherType appartient à l’en-tête Ethernet. Les registres IANA donnent les affectations, tandis que les services réels dépendent de leur configuration.

| Protocole / usage | Transport ou identifiant usuel | Repère |
| --- | --- | --- |
| IPv4 sur Ethernet | EtherType 0x0800 | Type de charge Ethernet |
| ARP | EtherType 0x0806 | Résolution IPv4 locale |
| IPv6 sur Ethernet | EtherType 0x86DD | Type de charge Ethernet |
| EAPOL | EtherType 0x888E | Accès 802.1X sur le lien |
| ICMPv4 | Protocole IP 1 | Diagnostic IPv4 |
| TCP | Protocole IP 6 | Transport avec état |
| UDP | Protocole IP 17 | Transport datagramme |
| IPv6-ICMP | Next Header 58 | ND et diagnostics IPv6 |
| OSPF | Protocole IP 89 | Absence de port TCP/UDP OSPF |
| EIGRP | Protocole IP 88 | Absence de port TCP/UDP EIGRP |
| ESP | Protocole IP 50 | IPsec hors encapsulation NAT-T |
| AH | Protocole IP 51 | Autre protocole de la suite IPsec |
| BGP | TCP 179 | Port serveur du peering |
| DNS classique | UDP/TCP 53 | Les deux transports sont utiles |
| DHCPv4 | UDP 67 serveur, 68 client | Relais à considérer |
| DHCPv6 | UDP 547 serveur, 546 client | Fonctionnement distinct de DHCPv4 |
| NTP | UDP 123 | Temps |
| SNMP | UDP 161/162 usuels | Requêtes / notifications |
| SSH | TCP 22 | Administration |
| HTTPS | TCP 443 courant | Des usages HTTP/3 utilisent QUIC sur UDP |
| IKE | UDP 500 | Négociation IPsec |
| ESP NAT-T | UDP 4500 | ESP encapsulé |
| RADIUS classique | UDP 1812/1813 | Authentification / accounting |
| RADIUS CoA/Disconnect | UDP 3799 | Autorisation dynamique |
| VXLAN | UDP destination 4789 | Vérifier les implémentations héritées |
| BFD single-hop | UDP 3784 | Contrôle de session single-hop |
| BFD echo | UDP 3785 | Fonction echo lorsque prise en charge |

Cette table facilite la lecture des paquets. Elle ne constitue pas une politique firewall à appliquer telle quelle.

- [IANA — numéros de protocoles](https://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml)
- [IANA — noms de services et ports](https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml)
- [IANA — paramètres IEEE 802](https://www.iana.org/assignments/ieee-802-numbers/ieee-802-numbers.xhtml)

[Retour au sommaire](../README.md)
