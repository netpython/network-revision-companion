# 16 · IS-IS, niveaux et TLV

[Fiche précédente](../03-ip-et-routage/15-eigrp.md) · [Sommaire](../../README.md) · [Fiche suivante](../03-ip-et-routage/17-bgp.md)

## Comprendre

IS-IS est un IGP à état de liens. Les informations sont transportées sous forme de TLV dans des LSP, puis SPF calcule les chemins. Integrated IS-IS permet d'annoncer des préfixes IP.

Les paquets de contrôle IS-IS sont transportés directement sur la couche liaison, et ne reposent pas sur TCP ou UDP. Le NET fournit notamment une identité de système et une composante de zone.

| Rôle | Domaine de connaissance |
| --- | --- |
| Level 1 | Routage au sein d'une zone L1 |
| Level 2 | Connectivité entre domaines à travers le niveau L2 |
| L1/L2 | Participe aux deux niveaux et les relie |

L1 et L2 désignent ici des niveaux du protocole, distincts des couches du modèle OSI. La connectivité L2 du domaine IS-IS doit être conçue comme un ensemble cohérent. Le leaking de routes modifie la visibilité entre niveaux et peut exiger des mécanismes anti-boucle spécifiques.

Sur réseau multi-accès, un DIS produit une représentation de pseudonœud. Contrairement au couple DR/BDR d'OSPF, il n'existe pas de backup DIS identique au BDR. L'élection est préemptive.

La base LSP et les échanges CSNP/PSNP participent à la synchronisation. Les extensions de métrique et de TLV permettent d'ajouter des informations selon les capacités et politiques du réseau.

## Exemple concret

Un routeur IS-IS L1 peut apprendre une sortie via un routeur L1/L2 sans connaître tous les détails du domaine L2. Une vue partielle peut donc être cohérente avec son rôle.

## Pièges à éviter

- Confondre Level 2 IS-IS et commutation Ethernet L2.
- Chercher un port TCP/UDP pour IS-IS.
- Transposer sans adaptation les règles DR/BDR d’OSPF.

## Ce qu’il faut observer

Vérifier NET et System ID, niveau et type de circuit, adjacency, LSP, métriques et installation des préfixes.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

IS-IS dépend-il d’un transport TCP ?

<details><summary>Afficher la correction</summary>

Non. Ses PDU de contrôle sont portées directement sur la liaison.

</details>

### Question 2

Un routeur L1/L2 participe-t-il aux deux bases de niveau ?

<details><summary>Afficher la correction</summary>

Il participe aux domaines L1 et L2 selon la configuration.

</details>

### Question 3

Existe-t-il un backup DIS équivalent au BDR OSPF ?

<details><summary>Afficher la correction</summary>

Non, les mécanismes ne sont pas identiques.

</details>

## Sources pour approfondir

- [RFC 1195](https://www.rfc-editor.org/rfc/rfc1195)
- [RFC 5305](https://www.rfc-editor.org/rfc/rfc5305)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
