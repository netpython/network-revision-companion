# Cas de synthèse

Explique le chemin et les preuves nécessaires avant d’ouvrir les corrections. Ces scénarios sont pédagogiques et ne représentent pas des captures réelles.

## 1. HTTPS fonctionne sur un poste, pas sur son voisin

Les deux postes sont dans le VLAN 20 et accèdent au même nom. Le premier reçoit seulement une adresse A. Le second reçoit A et AAAA et tente IPv6. Un ping IPv4 depuis le switch réussit.

Questions à traiter.

- Quel flux témoin faut-il définir ?
- Que prouve le ping depuis le switch ?
- Quelles différences de chemin faut-il vérifier ?

<details><summary>Correction et démarche</summary>

Définir client, IP effectivement choisie, port TCP et heure. Le ping teste une source et une famille différentes du second client. Comparer résolution, adresse et route IPv6, ND, politique et accès au service. Si le handshake fonctionne mais le transfert bloque, inclure PMTUD. Vérifier ensuite le même service et la même famille depuis le client.

</details>

## 2. MPLS L3VPN avec routes visibles mais trafic perdu

La route client existe dans la table VPN du PE-A avec un RD et un RT attendus. Elle est importée dans la VRF. Le next-hop correspond au PE-B.

Questions à traiter.

- Que prouvent RD et RT ?
- Quelles dépendances de forwarding restent à examiner ?
- Pourquoi l’absence de route client sur P peut-elle être normale ?

<details><summary>Correction et démarche</summary>

Le RD différencie la route et le RT participe à la politique d’import. Il faut encore joindre le PE-B, disposer du transport et du label VPN appropriés, résoudre le prochain saut client et valider le retour. Le routeur P assure le transport MPLS sans devoir connaître le préfixe client dans le modèle décrit.

</details>

## 3. VXLAN transporte les petits paquets

Deux VTEP se joignent. Un paquet IP client de 1500 octets est encapsulé en VXLAN sur IPv4 avec Ethernet intérieur non tagué. L’underlay a une IP MTU de 1500.

Questions à traiter.

- Quelle taille IP extérieure faut-il au minimum dans cet exemple ?
- Un ping VTEP de petite taille valide-t-il cette contrainte ?
- Que changent des tags ou encapsulations supplémentaires ?

<details><summary>Correction et démarche</summary>

1500 + Ethernet intérieur 14 + VXLAN 8 + UDP 8 + IPv4 extérieur 20 = 1550 octets d’IP extérieure. Une petite sonde ne valide pas cette taille. Les tags intérieurs, autres tunnels ou un IP extérieur IPv6 exigent de refaire le calcul. Identifier les signaux de MTU et adapter l’architecture plutôt que supposer que le tunnel actif suffit.

</details>

## 4. Un poste NAC est authentifié mais n’obtient aucun accès

Le serveur renvoie Access-Accept. Le switch applique un VLAN de quarantaine. Le client conserve son ancienne adresse.

Questions à traiter.

- Quel résultat correspond à l’authentification ?
- Quel résultat correspond à l’autorisation ?
- Quelles étapes IP doivent être vérifiées après le changement de rôle ?

<details><summary>Correction et démarche</summary>

Access-Accept décrit le résultat serveur, tandis que l’autorisation effective est le VLAN ou rôle appliqué. Lire la politique qui a conduit à ce rôle, puis l’état de la session. Vérifier le changement réel de VLAN, le renouvellement des paramètres IP, la passerelle et les permissions prévues. Une ancienne adresse peut maintenir une incohérence même après succès EAP.

</details>

## 5. BGP préfère un chemin à AS_PATH plus long

Deux chemins sont valides vers le même préfixe. Le premier a LOCAL_PREF 200 et AS_PATH plus long. Le second a LOCAL_PREF 100. La plateforme choisit le premier.

Questions à traiter.

- Pourquoi ce résultat peut-il être cohérent ?
- Que faut-il vérifier avant de prétendre expliquer l’ordre complet de sélection ?
- Quel lien existe entre meilleur BGP et forwarding ?

<details><summary>Correction et démarche</summary>

La politique interne peut préférer LOCAL_PREF 200 avant de comparer la longueur AS_PATH. Il faut confirmer les autres attributs, options et règles de la plateforme avant de raconter tout le meilleur chemin. Le meilleur candidat BGP doit aussi être retenu et installé correctement dans les tables du système. La RIB, la FIB et le next-hop doivent être vérifiés.

</details>

## 6. La gateway est redondante mais l’application reste coupée

R1 et R2 partagent une IP virtuelle. R1 perd une connectivité distante mais son port physique reste up. Son tracking surveille seulement le line protocol local.

Questions à traiter.

- Pourquoi R1 peut-il conserver son rôle ?
- Quel signal devrait représenter l’objectif de disponibilité ?
- Quelles dépendances partagées peuvent encore casser le service ?

<details><summary>Correction et démarche</summary>

Le signal surveillé n’a pas changé, donc la priorité peut rester identique. Le tracking doit représenter le service ou la route utile selon le design, avec des seuils et temporisations adaptés. Même avec bascule, examiner route de retour, état firewall/NAT, alimentation et points communs. Mesurer le trafic pendant le test établit la restauration réelle.

</details>

[Retour au sommaire](../README.md)
