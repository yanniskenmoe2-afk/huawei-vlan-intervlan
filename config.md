# ============================================================
# PROJET : Segmentation en VLAN et routage inter-VLAN avec VLANIF
# PLATEFORME : Huawei eNSP / Huawei VRP
#
# EXEMPLE DE PLAN D'ADRESSAGE
# VLAN 10 : 192.168.10.0/24 ; passerelle : 192.168.10.1
# VLAN 20 : 192.168.20.0/24 ; passerelle : 192.168.20.1
#
# PORTS UTILISES DANS CET EXEMPLE
# GE0/0/1 : poste du VLAN 10 (access)
# GE0/0/2 : poste du VLAN 20 (access)
# GE0/0/24 : lien trunk vers un autre switch (si présent)
#
# IMPORTANT :
# - Adapte les interfaces au modèle de switch utilisé dans eNSP.
# - Le routage VLANIF nécessite un switch Huawei de couche 3 compatible.
# - Si un seul switch est utilisé et qu'aucun autre switch n'est raccordé,
#   le trunk GE0/0/24 est facultatif.
# ============================================================

system-view
sysname SW-HUAWEI

# 1. CREATION DES VLAN
vlan batch 10 20

# 2. PORTS ACCESS
# Poste / équipement appartenant au VLAN 10
interface GigabitEthernet0/0/1
 port link-type access
 port default vlan 10
 quit

# Poste / équipement appartenant au VLAN 20
interface GigabitEthernet0/0/2
 port link-type access
 port default vlan 20
 quit

# 3. PORT TRUNK
# Exemple : liaison vers un autre switch transportant les VLAN 10 et 20
interface GigabitEthernet0/0/24
 port link-type trunk
 port trunk allow-pass vlan 10 20
 quit

# 4. INTERFACES VLANIF : PASSERELLES DES VLAN
interface Vlanif10
 ip address 192.168.10.1 255.255.255.0
 quit

interface Vlanif20
 ip address 192.168.20.1 255.255.255.0
 quit

# 5. SAUVEGARDE
return
save

# ============================================================
# COMMANDES DE VERIFICATION (à lancer en mode utilisateur <SW-HUAWEI>)
# ============================================================
# display vlan
# display port vlan
# display current-configuration
# display ip interface brief
# display interface GigabitEthernet0/0/1
# display interface GigabitEthernet0/0/2
# display interface GigabitEthernet0/0/24
#
# TESTS DEPUIS LES PC
# PC du VLAN 10 : IP 192.168.10.10/24, passerelle 192.168.10.1
# PC du VLAN 20 : IP 192.168.20.10/24, passerelle 192.168.20.1
# Depuis le PC VLAN 10, tester : ping 192.168.10.1 puis ping 192.168.20.10
#
# REMARQUES
# - Les adresses IP des PC sont des exemples à configurer sur les PC.
# - Pour que le ping inter-VLAN fonctionne, les VLANIF doivent être actifs
#   et les ports / liaisons doivent transporter les VLAN concernés.
# - Sur certains modèles, le nom des interfaces peut différer.
# ============================================================
