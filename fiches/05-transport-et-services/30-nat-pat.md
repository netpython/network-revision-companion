# 30 · NAT, PAT et lecture d’un flux traduit

[Fiche précédente](../05-transport-et-services/29-dhcp-dns-ntp.md) · [Sommaire](../../README.md) · [Fiche suivante](../05-transport-et-services/31-qos.md)

## Comprendre

NAT modifie des adresses IP et, selon la forme, des identifiants de transport. PAT partage une ou plusieurs adresses en différenciant les flux par ports ou autres identifiants adaptés au protocole.

| Forme | Usage typique |
| --- | --- |
| SNAT | Modifier l'identité source à la sortie |
| DNAT | Publier ou rediriger une destination |
| NAT statique | Association stable définie par configuration |
| PAT/overload | Mutualiser des adresses avec des identifiants de flux |

La traduction est un traitement du chemin. Il faut déterminer ce que chaque équipement observe avant et après transformation. L'ordre de routage, NAT et filtrage dépend de la plateforme et du type de trafic.

Un état de traduction ou de session est nécessaire dans de nombreux usages. Son vieillissement, sa capacité et sa synchronisation en haute disponibilité influencent les connexions existantes. Un chemin retour passant par un autre équipement peut ne pas retrouver le même état.

NAT ne remplace pas une politique firewall. Il peut masquer l'adressage tout en laissant des services exposés selon les règles. Les protocoles qui embarquent des adresses dans la charge ou vérifient certains champs peuvent exiger un traitement adapté.

Le dimensionnement concerne aussi le nombre de sessions et les ressources de ports disponibles, pas seulement la bande passante.

## Exemple concret

10.0.0.10:50000 vers 203.0.113.20:443 devient 198.51.100.2:61000 vers 203.0.113.20:443. La réponse doit retrouver la translation associée pour revenir vers le client interne.

## Pièges à éviter

- Déduire la sécurité du seul masquage d’adresses.
- Chercher uniquement le tuple privé sur le lien extérieur.
- Supposer le même ordre NAT/policy chez tous les constructeurs.

## Ce qu’il faut observer

Tracer les tuples avant/après, interfaces, route, règle et état de session. Vérifier temps de vie, saturation et asymétrie.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

PAT concerne-t-il seulement un changement d’adresse ?

<details><summary>Afficher la correction</summary>

Il utilise aussi des identifiants de flux, notamment les ports TCP/UDP.

</details>

### Question 2

Pourquoi une bascule peut-elle casser une session NAT existante ?

<details><summary>Afficher la correction</summary>

Le nouvel équipement peut ne pas disposer de l’état de traduction nécessaire.

</details>

### Question 3

Une règle NAT autorise-t-elle forcément le flux ?

<details><summary>Afficher la correction</summary>

Non. La politique de filtrage et les routes doivent aussi le permettre.

</details>

## Sources pour approfondir

- [RFC 3022](https://www.rfc-editor.org/rfc/rfc3022)
- [RFC 4787](https://www.rfc-editor.org/rfc/rfc4787)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
