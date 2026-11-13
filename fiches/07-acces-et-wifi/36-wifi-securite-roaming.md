# 36 · Wi-Fi, association, sécurité et roaming

[Fiche précédente](../07-acces-et-wifi/35-wifi-radio.md) · [Sommaire](../../README.md) · [Fiche suivante](../08-exploitation/37-observabilite.md)

## Comprendre

Une connexion Wi-Fi combine découverte du réseau, procédures 802.11, établissement de sécurité et services IP. Une association à un AP ne prouve pas qu'un client dispose d'un bail valide ou d'une autorisation utile.

Le SSID est le nom du service, le BSSID identifie une instance radio de cellule. Un même SSID peut être proposé par plusieurs BSSID. La sécurité dépend de la méthode d'authentification, des paramètres de chiffrement et de la validation du client.

| Mécanisme | Contribution au roaming |
| --- | --- |
| 802.11k | Informations de voisinage et mesures |
| 802.11v | Assistance à la gestion et à la transition |
| 802.11r | Fast BSS Transition pour réduire certains délais de sécurité |

Le terminal décide généralement de son changement d'AP selon ses propres critères. Le réseau peut l'informer, l'encourager ou appliquer des politiques, mais le résultat dépend du support client. Une couverture qui se chevauche ne suffit pas à garantir une transition de bonne qualité.

WPA2/WPA3 regroupent des ensembles de mécanismes et de modes. Enterprise utilise typiquement 802.1X/EAP. Le rôle de la protection des trames de gestion et les compatibilités doivent être vérifiés pour le mode retenu.

Après un roaming, le maintien de l'adresse et des sessions dépend de l'architecture L2/L3, du contrôleur et de la mobilité du service. Une interruption peut venir de la radio, de l'authentification ou du réseau IP.

## Exemple concret

Un téléphone passe de BSSID-A à BSSID-B et conserve son SSID. Une coupure voix de plusieurs secondes peut provenir d'une réauthentification, d'un mauvais déclenchement radio ou d'un changement de contexte IP. Il faut séparer ces étapes.

## Pièges à éviter

- Confondre SSID et BSSID.
- Supposer que 802.11k/v/r est pris en charge par tous les terminaux.
- Déduire le maintien des sessions du seul maintien du nom de réseau.

## Ce qu’il faut observer

Corréler changements de BSSID, méthode d’authentification, timing de roaming, adresse IP, rôle et paquets du flux métier.

## Révision active

Réponds à voix haute avant d’ouvrir chaque correction.

### Question 1

Quel identifiant change lors d’un passage vers une autre cellule ?

<details><summary>Afficher la correction</summary>

Le BSSID peut changer alors que le SSID reste identique.

</details>

### Question 2

802.11r garantit-il un roaming sans perte pour tout terminal ?

<details><summary>Afficher la correction</summary>

Non. Support, configuration, radio et architecture restent déterminants.

</details>

### Question 3

Pourquoi distinguer association et accès applicatif ?

<details><summary>Afficher la correction</summary>

La sécurité, les paramètres IP et le chemin du service interviennent après ou autour de l’association.

</details>

## Sources pour approfondir

- [Documentation de référence 1](https://www.ieee802.org/11/)
- [Documentation de référence 2](https://www.wi-fi.org/discover-wi-fi/security)
- [Documentation de référence 3](https://arubanetworking.hpe.com/techdocs/new-central-review/content/cfg/profiles/wlan-prof-cnx.htm)

Les mécanismes décrits servent à réviser. Les détails CLI et les limites de produit doivent être vérifiés dans la documentation de la version utilisée.
