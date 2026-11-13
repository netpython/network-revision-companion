# 18 · MP-BGP, AFI/SAFI et familles de routes

[Fiche précédente](../03-ip-et-routage/17-bgp.md) · [Sommaire](../../README.md) · [Fiche suivante](../03-ip-et-routage/19-redistribution-filtrage.md)

## Comprendre

Les extensions multiprotocoles de BGP permettent de transporter différentes familles d'informations de joignabilité. AFI identifie une famille d'adresses et SAFI précise le type d'information. Les capabilities échangées indiquent les familles négociées.

| Famille | Information portée |
| --- | --- |
| IPv4/IPv6 unicast | Préfixes IP unicast |
| VPNv4/VPNv6 | Préfixes VPN distingués par RD |
| L2VPN EVPN | Routes de contrôle de services Ethernet et overlays |

MP_REACH_NLRI transporte des informations de joignabilité avec un next-hop, et MP_UNREACH_NLRI des retraits. Les formats de NLRI et de next-hop dépendent de la famille. Les extended communities et autres attributs associés donnent du sens au service.

Une session TCP BGP peut être établie alors qu'une famille n'est pas activée ou négociée. Les politiques import/export peuvent également différer par famille. Il faut interroger la table correspondant au service recherché.

MP-BGP est un transport de contrôle. Il ne constitue pas à lui seul l'encapsulation de données. Une route VPNv4 ou EVPN doit être accompagnée des mécanismes de forwarding nécessaires, comme MPLS ou VXLAN selon l'architecture.

## Exemple concret

Deux PE disposent d'une session BGP IPv4 unicast saine mais n'échangent aucune route VPNv4. Vérifier l'activation et la négociation de VPNv4 est une étape distincte du contrôle de la session TCP.

## Pièges à éviter

- Supposer qu’une session BGP active transporte toutes les familles.
- Assimiler AFI/SAFI à un simple numéro de version IP.
- Confondre distribution de routes et transport du trafic client.

## Ce qu’il faut observer

Contrôler capabilities, activation de famille, NLRI, communautés, next-hop et table de destination du service.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

Une session établie prouve-t-elle EVPN opérationnel ?

<details><summary>Afficher la correction</summary>

Non. EVPN doit être négocié, activé et alimenté avec des routes pertinentes.

</details>

### Question 2

Quel rôle joue MP_UNREACH_NLRI ?

<details><summary>Afficher la correction</summary>

Il transporte des retraits de joignabilité pour la famille concernée.

</details>

### Question 3

MP-BGP chiffre-t-il le trafic client ?

<details><summary>Afficher la correction</summary>

Non. Le contrôle de routage et la protection ou l’encapsulation des données sont des fonctions distinctes.

</details>

## Sources pour approfondir

- [RFC 4760](https://www.rfc-editor.org/rfc/rfc4760)
- [RFC 4364](https://www.rfc-editor.org/rfc/rfc4364)
- [RFC 7432](https://www.rfc-editor.org/rfc/rfc7432)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
