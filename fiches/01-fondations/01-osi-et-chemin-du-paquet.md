# 01 · OSI, encapsulation et chemin d’un paquet

[Sommaire](../../README.md) · [Fiche suivante](../01-fondations/02-cuivre-fibre-optique-poe.md)

## Comprendre

Le modèle OSI sert à situer les fonctions d'un échange. L1 transporte les signaux, L2 livre les trames sur un lien, L3 permet de traverser des réseaux et L4 transporte les échanges entre extrémités. La pile Internet n'épouse pas exactement les sept couches OSI.

| Couche | Objet manipulé | Identifiant utile | Question de diagnostic |
| --- | --- | --- | --- |
| L1 | Signal, bits | Port, média | Le lien fonctionne-t-il correctement ? |
| L2 | Trame | MAC, VLAN | Le prochain saut est-il joignable sur ce lien ? |
| L3 | Paquet | IP, préfixe, VRF | Quel chemin mène au réseau destination ? |
| L4 | Segment/datagramme | Ports, état TCP | Le service de transport répond-il ? |

Une application remet ses données à TCP ou UDP. IP ajoute l'adressage réseau. Ethernet ou Wi-Fi fournit l'accès au lien. Un routeur retire l'enveloppe du lien entrant, recherche le prochain saut et construit celle du lien sortant. Les adresses MAC changent généralement à chaque saut routé. Les adresses IP des extrémités restent les mêmes en l'absence de NAT ou de terminaison intermédiaire.

Le TTL IPv4 ou Hop Limit IPv6 limite la durée de vie du paquet. Un switch L2 ne décrémente pas ce champ. Les tunnels ajoutent une enveloppe extérieure dont les adresses décrivent leurs extrémités.

## Exemple concret

Un PC envoie vers un serveur hors de son sous-réseau. Il cherche la MAC de sa passerelle et lui adresse la trame. L'IP destination reste celle du serveur. Recevoir une trame destinée à sa MAC ne signifie donc pas que le routeur est le destinataire IP.

## Pièges à éviter

- Associer strictement chaque équipement à une couche unique.
- Déduire le fonctionnement de TCP d’un simple ping.
- Confondre adresse du prochain saut et adresse du destinataire final.

## Ce qu’il faut observer

Relever IP source/destination, MAC source/destination, VLAN, TTL et ports à deux points du chemin. Comparer des captures du même flux.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

Pourquoi la MAC destination est-elle celle de la passerelle ?

<details><summary>Afficher la correction</summary>

La destination IP est hors lien local. La passerelle est le prochain saut Ethernet.

</details>

### Question 2

Un switch décrémente-t-il le TTL en commutation L2 ?

<details><summary>Afficher la correction</summary>

Non. La décrémentation correspond à un transfert IP routé.

</details>

### Question 3

Une capture extérieure d’un tunnel montre-t-elle directement les adresses internes ?

<details><summary>Afficher la correction</summary>

Cela dépend de l’encapsulation et du chiffrement. Les en-têtes extérieurs identifient les extrémités du tunnel.

</details>

## Sources pour approfondir

- [RFC 1122](https://www.rfc-editor.org/rfc/rfc1122)
- [RFC 8200](https://www.rfc-editor.org/rfc/rfc8200)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
