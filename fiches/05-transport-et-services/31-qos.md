# 31 · QoS, DSCP, files, policing et shaping

[Fiche précédente](../05-transport-et-services/30-nat-pat.md) · [Sommaire](../../README.md) · [Fiche suivante](../06-securite-et-sdwan/32-acl-firewall-ipsec.md)

## Comprendre

La QoS applique un traitement différencié aux paquets. Elle commence par la classification, puis peut marquer, mettre en file, ordonnancer, limiter ou éliminer des paquets selon une politique.

| Mécanisme | Effet |
| --- | --- |
| Classification | Reconnaître la catégorie de trafic |
| Marquage | Porter une indication comme DSCP |
| Queuing/scheduling | Choisir l'ordre de service sous concurrence |
| Policing | Faire respecter un profil, avec drop ou remark selon politique |
| Shaping | Retarder des paquets pour lisser le débit de sortie |

DSCP utilise six bits du champ DS dans l'en-tête IP. ECN exploite les deux autres bits du champ pour une signalisation de congestion selon les capacités. Le marquage doit être compris et respecté par les équipements pour produire un effet utile.

La confiance accordée aux marquages clients doit être explicitée. Une priorité stricte sans maîtrise de volume peut défavoriser d'autres classes. Les pourcentages de bande passante dépendent du niveau de politique et de la plateforme.

La QoS ne crée pas de capacité supplémentaire. Elle organise l'usage d'une ressource, surtout lors de congestion. Le shaping doit tenir compte du débit réellement disponible et de l'overhead du lien. Un compteur de classe prouve une classification, pas nécessairement une amélioration applicative.

## Exemple concret

Un lien vendu à 100 Mbit/s subit un policing opérateur. Un shaping local adapté peut déplacer l'attente vers des files maîtrisées par l'entreprise. Le réglage exact exige de connaître le profil et le mode de comptage opérateur.

## Pièges à éviter

- Croire qu’un DSCP élevé garantit une priorité partout.
- Confondre policing et shaping.
- Évaluer une politique de files sans trafic concurrent.

## Ce qu’il faut observer

Mesurer débit, drops, profondeur de file et latence par classe, sur un intervalle défini et à charge comparable.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

Le shaping retarde-t-il ou élimine-t-il toujours immédiatement l’excédent ?

<details><summary>Afficher la correction</summary>

Il utilise de la mise en attente dans ses limites. Des pertes restent possibles si les buffers sont dépassés.

</details>

### Question 2

Que signifie une hausse du compteur de classe ?

<details><summary>Afficher la correction</summary>

Que des paquets ont été classifiés, sans prouver le résultat applicatif.

</details>

### Question 3

Combien de bits porte DSCP ?

<details><summary>Afficher la correction</summary>

Six bits.

</details>

## Sources pour approfondir

- [RFC 2474](https://www.rfc-editor.org/rfc/rfc2474)
- [RFC 2475](https://www.rfc-editor.org/rfc/rfc2475)
- [RFC 3168](https://www.rfc-editor.org/rfc/rfc3168)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
