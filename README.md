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
![cs1](https://user-images.githubusercontent.com/85891554/146661410-e8f40936-3b69-4481-ad35-7f418c9cc1c6.png)

- Dans la manipulation précédente, les trames sont affichées sous format hexadécimal. Pour afficher le contenu de l’entête ETHERNET, il faut enlever le commentaire de la fonction ParseEthernetHeader, recompiler, régénérer l’exécutable et refaire l’étape 2). 

![cs2 (2)](https://user-images.githubusercontent.com/85891554/146661437-1deb99a6-18ed-486e-8140-81d1594cb26a.png)

- Pour Afficher le contenu des entêtes des protocoles des niveaux supérieurs, enlevez les commentaires des fonctions correspondantes (au niveau de la fonction main), recompiler, régénérer l’exécutable et exécuter de nouveau le sniffer. Pensez à faire un échange de trafic TCP (en utilisant par exemple le serveur vsftpd ou en se connectant à Internet). 

![cs3](https://user-images.githubusercontent.com/85891554/146661515-f08c9c1f-fb01-458e-8e3b-e3d87eac5f62.png)
![cs4](https://user-images.githubusercontent.com/85891554/146661526-33f22e78-7031-477b-96d9-b46bac64b048.png)

- Ecrire une fonction qui permet d’afficher l’entête UDP et l’intégrer dans le code source du sniffer (localiser udp.h dans /usr/include/netinet). 

![cs5](https://user-images.githubusercontent.com/85891554/146661528-490b5e6d-2e9e-4cbc-bd2a-877096718c7f.png)

![cs6](https://user-images.githubusercontent.com/85891554/146661529-f0568fa0-0b80-4063-be49-c2035d8e9a5d.png)

![cs7](https://user-images.githubusercontent.com/85891554/146661531-b0f19212-4e8e-4ea0-8cec-59b918f7bc19.png)
 
 # Partie 2 : manipulation de sniffers 

Dans cette partie, nous nous intéressons à la manipulation de quelques sniffers existants. 

- Lancer le logiciel wireshark en arrière- plan (wireshark &) et commencez la capture sur l’interface ETHERNET ou sans fil. 

