# 12 · ARP, Neighbor Discovery et ICMP

[Fiche précédente](../03-ip-et-routage/11-ipv6.md) · [Sommaire](../../README.md) · [Fiche suivante](../03-ip-et-routage/13-rib-fib-et-selection.md)

## Comprendre

ARP résout une adresse IPv4 vers une adresse de lien sur un réseau local. Pour une destination hors sous-réseau, la résolution concerne le prochain saut local. Le cache ARP associe les réponses reçues à une interface et un contexte réseau.

Neighbor Discovery remplit plusieurs fonctions en IPv6, dont découverte de voisins, de routeurs et vérification de joignabilité. Les Neighbor Solicitations et Advertisements s'appuient sur ICMPv6 et sur des adresses multicast adaptées. DAD détecte certains conflits d'adresse avant une utilisation normale.

| Fonction | IPv4 | IPv6 |
| --- | --- | --- |
| Résolution de voisin | ARP | Neighbor Discovery |
| Erreurs et diagnostic | ICMP | ICMPv6 |
| Expiration en transit | TTL | Hop Limit |

ICMP transporte des diagnostics comme destination unreachable et time exceeded. Ping exploite echo request/reply. Traceroute fait varier la durée de vie pour obtenir des réponses intermédiaires. Selon l'outil, ses probes peuvent être UDP, ICMP ou TCP.

Une réponse ICMP dépend des politiques et du traitement du plan de contrôle. Un routeur peut limiter ses propres réponses tout en transférant les paquets des utilisateurs. À l'inverse, un ping réussi vers un équipement ne prouve pas le transfert du flux applicatif à travers lui.

## Exemple concret

Une table ARP vide pour la passerelle peut indiquer un VLAN incorrect, un lien coupé ou simplement l'absence de tentative. Générer un paquet puis observer la requête et la réponse permet de distinguer ces cas.

## Pièges à éviter

- Chercher la MAC du serveur distant à la place de celle de la passerelle.
- Interpréter chaque étoile traceroute comme une panne du chemin.
- Utiliser la présence d’une entrée ARP comme preuve de service applicatif.

## Ce qu’il faut observer

Comparer sollicitations, réponses, états du cache, IP/MAC et interface. Sur traceroute, examiner le résultat final et les limites de réponse intermédiaires.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

ARP traverse-t-il normalement un routeur ?

<details><summary>Afficher la correction</summary>

La résolution ARP est locale au lien. Les mécanismes comme proxy ARP sont des comportements spécifiques supplémentaires.

</details>

### Question 2

Pourquoi bloquer ICMP peut-il casser autre chose que ping ?

<details><summary>Afficher la correction</summary>

ICMP et ICMPv6 portent des erreurs et des informations nécessaires, notamment pour PMTUD.

</details>

### Question 3

Que prouve une réponse echo ?

<details><summary>Afficher la correction</summary>

Une joignabilité ICMP pour ce test précis, avec ses adresses et politiques.

</details>

## Sources pour approfondir

- [RFC 826](https://www.rfc-editor.org/rfc/rfc826)
- [RFC 4861](https://www.rfc-editor.org/rfc/rfc4861)
- [RFC 792](https://www.rfc-editor.org/rfc/rfc792)
- [RFC 4443](https://www.rfc-editor.org/rfc/rfc4443)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
