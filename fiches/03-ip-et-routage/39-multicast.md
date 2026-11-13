# 39 · Multicast, IGMP, MLD et PIM

[Fiche précédente](../08-exploitation/38-diagnostic-transversal.md) · [Sommaire](../../README.md) · [Fiche suivante](../03-ip-et-routage/40-resilience-fhrp-bfd.md)

## Comprendre

Le multicast livre des paquets à un groupe de récepteurs intéressés. Les hôtes signalent leur appartenance avec IGMP en IPv4 ou MLD en IPv6. Le routage multicast construit des états et arbres adaptés aux sources et groupes.

| Mécanisme | Rôle |
| --- | --- |
| IGMP / MLD | Adhésion des récepteurs sur un lien |
| Snooping | Adapter la réplication L2 aux informations de groupe |
| PIM | Construire le routage multicast selon le mode |
| RPF | Vérifier la cohérence de l'interface d'entrée vers la source |

En PIM Sparse Mode ASM, un rendezvous point intervient dans la découverte et les arbres partagés selon le fonctionnement. En SSM, le récepteur demande explicitement un couple source/groupe, avec IGMPv3 ou MLDv2 adaptés.

Le snooping ne remplace pas le routage multicast. La présence d'un querier participe à la maintenance des appartenances sur le LAN. Un VLAN peut diffuser davantage de multicast si les informations nécessaires manquent.

La vérification RPF s'appuie sur la vue de routage utilisée pour atteindre la source, selon la plateforme et la configuration. Un paquet entrant sur une interface inattendue peut être rejeté malgré des routes unicast apparemment saines. La bonne source doit être distinguée du groupe destination.

## Exemple concret

Un flux (S,G) entre sur un lien de secours alors que le chemin RPF vers S pointe vers le primaire. La réception peut échouer. Il faut examiner l'état multicast et le choix RPF, pas seulement un ping vers le groupe.

## Pièges à éviter

- Chercher le groupe destination comme s’il s’agissait d’une route unicast ordinaire.
- Confondre snooping et routage.
- Oublier le rôle du querier et des temporisations d’adhésion.

## Ce qu’il faut observer

Vérifier adhésion des clients, groupe/source, querier, interfaces entrantes/sortantes, arbre et RPF. Comparer avec le routage vers la source.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

IGMP route-t-il les paquets entre sous-réseaux ?

<details><summary>Afficher la correction</summary>

Il signale les appartenances IPv4 sur le lien. Le routage est une autre fonction.

</details>

### Question 2

Que représente (S,G) ?

<details><summary>Afficher la correction</summary>

Un couple source et groupe multicast.

</details>

### Question 3

SSM exige-t-il un RP pour la découverte ASM ?

<details><summary>Afficher la correction</summary>

Le modèle SSM connaît la source demandée et n’utilise pas ce mécanisme ASM de découverte par RP.

</details>

## Sources pour approfondir

- [RFC 3376](https://www.rfc-editor.org/rfc/rfc3376)
- [RFC 3810](https://www.rfc-editor.org/rfc/rfc3810)
- [RFC 7761](https://www.rfc-editor.org/rfc/rfc7761)
- [RFC 4607](https://www.rfc-editor.org/rfc/rfc4607)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
