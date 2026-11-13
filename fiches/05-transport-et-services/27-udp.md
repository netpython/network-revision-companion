# 27 · UDP et responsabilité de l’application

[Fiche précédente](../05-transport-et-services/26-tcp.md) · [Sommaire](../../README.md) · [Fiche suivante](../05-transport-et-services/28-mtu-mss-pmtud.md)

## Comprendre

UDP transporte des datagrammes avec un en-tête de huit octets comprenant ports source/destination, longueur et checksum. Il préserve les frontières des datagrammes reçus, mais ne fournit pas lui-même établissement, acquittement, retransmission ou contrôle de congestion équivalent à TCP.

Une application au-dessus d'UDP peut ajouter fiabilité, ordonnancement, chiffrement et contrôle de congestion. QUIC en est un exemple, avec ses propres mécanismes. Choisir UDP ne signifie donc pas que toute application renonce à la fiabilité.

| Observation | Limite d'interprétation |
| --- | --- |
| Datagramme envoyé | Ne prouve pas sa réception |
| Absence de réponse | Peut correspondre à un service silencieux ou filtré |
| ICMP unreachable | Indique une erreur selon le contexte et le filtrage |
| Flux bidirectionnel | Ne prouve pas à lui seul un résultat applicatif |

Le checksum est obligatoire dans les usages IPv6 ordinaires, avec des exceptions spécifiques définies pour certains tunnels. Il peut être omis dans le fonctionnement IPv4 UDP historique par une valeur nulle. Les applications doivent également tenir compte des tailles maximales et du risque de fragmentation.

Le comportement d'une application UDP doit être évalué avec son protocole propre. Le réseau peut être sain et l'application ne pas répondre à un paquet mal formé.

## Exemple concret

Une requête DNS en UDP reçoit une réponse marquée tronquée. Le client peut poursuivre avec TCP. Dire « DNS utilise uniquement UDP » conduit à une mauvaise règle de filtrage.

## Pièges à éviter

- Interpréter un port UDP sans réponse comme une preuve certaine de fermeture.
- Supposer qu’UDP interdit toute fiabilité applicative.
- Oublier les tailles et les dépendances d’un protocole applicatif.

## Ce qu’il faut observer

Identifier le format des datagrammes, les réponses attendues et les erreurs ICMP. Observer le service plutôt qu’un test UDP générique isolé.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

UDP réalise-t-il un handshake de transport ?

<details><summary>Afficher la correction</summary>

Non. L’application peut toutefois définir ses propres échanges d’établissement.

</details>

### Question 2

QUIC utilise-t-il UDP pour renoncer à toute retransmission ?

<details><summary>Afficher la correction</summary>

Non. QUIC définit notamment sa propre fiabilité et son contrôle de congestion.

</details>

### Question 3

Pourquoi un firewall peut-il suivre une session UDP ?

<details><summary>Afficher la correction</summary>

Il peut maintenir un état de flux et des temporisations, même sans handshake UDP.

</details>

## Sources pour approfondir

- [RFC 768](https://www.rfc-editor.org/rfc/rfc768)
- [RFC 8085](https://www.rfc-editor.org/rfc/rfc8085)
- [RFC 9000](https://www.rfc-editor.org/rfc/rfc9000)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
