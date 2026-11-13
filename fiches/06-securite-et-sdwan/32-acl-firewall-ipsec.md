# 32 · ACL, firewall stateful et IPsec

[Fiche précédente](../05-transport-et-services/31-qos.md) · [Sommaire](../../README.md) · [Fiche suivante](../06-securite-et-sdwan/33-sdwan.md)

## Comprendre

Une ACL stateless évalue des champs selon l'ordre de ses règles. Un firewall stateful associe les paquets à des états de connexion ou de flux et applique des politiques plus riches selon le produit.

Le retour d'un échange doit être analysé avec la direction et le point d'application. Pour UDP, un état peut être maintenu avec des temporisations même sans handshake. Les politiques NAT et de filtrage doivent être comprises dans l'ordre applicable à la plateforme.

| IPsec | Rôle |
| --- | --- |
| IKEv2 | Authentifier et négocier les associations de sécurité |
| ESP | Protéger le trafic selon le mode et les algorithmes |
| SA | État et paramètres de sécurité d'un sens de traitement |
| Sélecteurs | Définir le trafic ou les politiques concernés |

IKE utilise couramment UDP 500. NAT-T transporte ESP sur UDP 4500. ESP sans cette encapsulation utilise le numéro de protocole IP 50, qui n'est pas un port. Le mode tunnel protège un paquet interne avec une enveloppe extérieure. Le mode transport a une portée différente.

Une SA établie prouve une partie du contrôle, pas le bon transfert de chaque flux. Routes, NAT, sélecteurs, filtrage, MTU et chemin retour restent essentiels. Les mécanismes anti-replay peuvent rejeter des paquets selon leur séquencement et leur fenêtre.

## Exemple concret

Le tunnel est up et le compteur de chiffrement augmente sur A. Le compteur de déchiffrement sur B reste fixe. Il faut examiner le transport externe et les paquets reçus avant d'accuser l'application.

## Pièges à éviter

- Parler de « port ESP 50 ».
- Considérer le tunnel up comme une recette complète.
- Partager PSK ou clés privées dans une collecte.

## Ce qu’il faut observer

Identifier tuple avant/après NAT, politique effective et compteurs dans les deux sens pendant une tentative précise.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

Quel est le numéro IP d’ESP ?

<details><summary>Afficher la correction</summary>

50. Il identifie un protocole IP, pas un port TCP ou UDP.

</details>

### Question 2

Pourquoi une ACL stateless peut-elle bloquer un echo-reply ?

<details><summary>Afficher la correction</summary>

Le retour doit satisfaire ses propres conditions à son point d’application.

</details>

### Question 3

NAT-T utilise-t-il généralement UDP 4500 ?

<details><summary>Afficher la correction</summary>

Oui pour l’encapsulation ESP correspondante, selon la négociation et le contexte.

</details>

## Sources pour approfondir

- [RFC 4301](https://www.rfc-editor.org/rfc/rfc4301)
- [RFC 4303](https://www.rfc-editor.org/rfc/rfc4303)
- [RFC 7296](https://www.rfc-editor.org/rfc/rfc7296)
- [RFC 3948](https://www.rfc-editor.org/rfc/rfc3948)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
