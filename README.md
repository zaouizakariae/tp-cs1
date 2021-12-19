# tp-cs1
# ATTAQUES PASSIVES : SNIFFING PASSIF
## Résumé

Un sniffer (appelé aussi « analyseur de protocole » ou « analyseur de réseau ») est un outil logiciel qui permet de capturer des trames qui se propagent sur le réseau local et d'afficher leur contenu (en-tête de protocole, identité de l'utilisateur, mot de passe non crypté Wait). Les administrateurs utilisent ces outils pour analyser leurs réseaux et y localiser les problèmes. Les attaquants les utilisent également pour surveiller les données circulant dans le réseau local.

## 1-Objectifs de ce TP: 
-	Implémenter un sniffer passif simple 
-	Manipuler des logiciels de sniffing  
## 2-Outils logiciels: 
-	Linux, wireshark, compilateur cc ou gcc.
## 3-Partie 1 : Manipulations à faire (sous UBUNTU ) :
- Compiler (cc -c sniffer_eth_ip_tcp_data.c) le code source et générer l’exécutable (cc sniffer_eth_ip_tcp_data.c – o sniffer). 
```
cc -c sniffer_eth_ip_tcp_data.c
```
>_générer l’exécutable_ 
```
cc sniffer_eth_ip_tcp_data.c -o sniffer
```
- Exécuter (en mode root : « sudo commande » sous ubuntu) le sniffer (exemple : pour sniffer les 100 premières trames reçu sur l’interface eth0 tapez ./sniffer eth0 100). Vous pouvez utiliser wlan0 à la place de eth0 si vous êtes connecté en sans-fil (les trames Wifi sont automatiquement traduites en ETHERNET) ou lo (loopback) si vous n'avez aucune connexion. Si rien ne s’affiche, cela veut dire que vous n’êtes pas en train de recevoir des paquets, exécuter alors (dans une nouvelle fenêtre) un ping vers une autre machine et consulter de nouveau le résultat du sniffer.
```
sudo ./sniffer eth0 100
```
