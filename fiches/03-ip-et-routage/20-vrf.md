# 20 · VRF, VRF-Lite et route leaking

[Fiche précédente](../03-ip-et-routage/19-redistribution-filtrage.md) · [Sommaire](../../README.md) · [Fiche suivante](../04-mpls-et-overlays/21-mpls.md)

## Comprendre

Une VRF maintient un contexte de routage séparé. Deux VRFs peuvent contenir le même préfixe avec des next-hops et interfaces distincts. Les recherches et services doivent être exécutés dans le contexte approprié.

VRF-Lite fournit cette séparation sur des équipements sans exiger un cœur MPLS. Les interfaces relient les domaines selon un câblage ou une encapsulation adaptée. Une VRF peut être associée à des familles IPv4 et IPv6 selon le produit.

| Élément | Ce qu'il sépare |
| --- | --- |
| VLAN | Domaine de commutation/broadcast |
| VRF | Tables et contexte de routage |
| RD | Identité de préfixe VPN dans le contrôle |
| RT | Politique d'import/export VPN |

Un VLAN ne crée pas automatiquement une VRF. Plusieurs VLANs peuvent être routés dans la même VRF. À l'inverse, des interfaces routées ou sous-interfaces peuvent être affectées à des VRFs indépendantes.

Le route leaking introduit une connectivité entre contextes. Il doit préciser les préfixes, le sens, les next-hops et le chemin retour. Donner une route ne crée pas nécessairement une politique de sécurité adaptée ni les services DNS requis.

Le plan de gestion est également à considérer. Une adresse de gestion dans une VRF ne garantit pas qu'un service écoute ou que sa route de retour utilise ce contexte.

## Exemple concret

BLUE et RED utilisent 10.10.10.0/24. Un ping global échoue tandis qu'un ping dans BLUE réussit. Ce résultat peut être normal. Il faut identifier le contexte de la recherche avant de modifier le routage.

## Pièges à éviter

- Confondre séparation des routes et chiffrement.
- Oublier le contexte VRF dans une collecte.
- Créer un leaking sans vérifier le retour et le filtrage.

## Ce qu’il faut observer

Vérifier appartenance des interfaces, routes et voisins par VRF, next-hop, services associés et politiques entre domaines.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

Deux VRFs peuvent-elles utiliser le même préfixe ?

<details><summary>Afficher la correction</summary>

Oui, la séparation des contextes le permet.

</details>

### Question 2

Une VRF implique-t-elle MPLS ?

<details><summary>Afficher la correction</summary>

Non. VRF-Lite sépare le routage sans imposer un transport MPLS.

</details>

### Question 3

Une route importée garantit-elle l’accès au service ?

<details><summary>Afficher la correction</summary>

Non. Le retour, le filtrage, la résolution et les dépendances applicatives restent à vérifier.

</details>

## Sources pour approfondir

- [RFC 4364](https://www.rfc-editor.org/rfc/rfc4364)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
