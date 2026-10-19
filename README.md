# huawei-vlan-intervlan

# Configuration de deux VLAN et routage inter-VLAN — Huawei eNSP

## Présentation
Ce TP consiste à segmenter un réseau local en deux VLAN avec des équipements Huawei simulés dans eNSP, puis à permettre la communication entre ces VLAN grâce aux interfaces logiques **VLANIF**.

## Objectifs
Sur deux switchs(sw1 et sw2), 
- Créer et nommer deux VLAN.
- Affecter les ports du commutateur aux VLAN correspondants.
- Configurer les interfaces VLANIF et leurs adresses IP(uniquement sur un switch pour eviter les conflits ).
- Vérifier la connectivité entre les réseaux.

## Principe de fonctionnement
Un VLAN sépare logiquement les équipements en domaines de diffusion distincts. Les interfaces VLANIF fournissent des interfaces de couche 3 associées aux VLAN et permettent le routage entre leurs sous-réseaux(vlans differents), lorsque l’équipement le prend en charge.

## Étapes principales
1. Construire la topologie dans Huawei eNSP.
2. Créer les deux VLAN.
3. Affecter les ports aux VLAN appropriés.
4. Configurer une interface VLANIF par VLAN avec une adresse IP.
5. Configurer les adresses IP et les passerelles des postes.
6. Tester avec `ping` entre les postes et vérifier la configuration.

## Vérifications utiles
```text
display vlan
display ip interface brief
display current-configuration
ping <adresse_IP_destination>(exemple: 192.168.20.10)
```

## Résultat attendu
Les équipements d’un même VLAN communiquent entre eux. Les équipements de VLAN différents peuvent communiquer si les VLANIF, les adresses IP et les passerelles sont correctement configurées et si l’équipement assure le routage de couche 3.

## Méthode alternative
Une autre méthode courante est le **Router-on-a-Stick** : un routeur utilise une interface physique en trunk et des sous-interfaces associées aux VLAN pour assurer le routage inter-VLAN.

## Compétences démontrées
- Segmentation logique d’un LAN.
- Configuration VLAN sur équipement Huawei.
- Routage inter-VLAN avec VLANIF.
- Tests et diagnostic de connectivité.

## Environnement
- Simulateur : Huawei eNSP
- Technologies : VLAN, VLANIF, IPv4


