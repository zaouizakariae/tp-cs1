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

![cs11](https://user-images.githubusercontent.com/85891554/146661790-4b9ea5bc-edcb-4a41-a575-541e10c714b0.png)
![cs12](https://user-images.githubusercontent.com/85891554/146661794-390beed0-1f59-402e-bb7c-0d4320299593.png)

- Lancez des applications d’échange de trafic entre d'autres machines et la votre. Observez-les paquets capturés

![cs13](https://user-images.githubusercontent.com/85891554/146661798-91cf5687-829a-4c72-8e10-4d093bcaabbd.png)

- Est-ce que vous pouvez capturer les trafics échangés entre les machines du reste du réseau? 
  - Oui, les trafics échangés entre les machines du reste du réseau sont capturés. Si on effectue par exemple un Ping entre la machine virtuelle Windows (192.168.1.4) et Ubuntu (192.168.1.3) on peut capturer les paquets envoyés sur wireshark à partir de la machine virtuelle Kali

![cs21](https://user-images.githubusercontent.com/85891554/146661880-a2e4e896-2c9d-4039-abc0-8a1c0482f19a.png)

- Configurer le filtre de wireshark pour (voir annexe 2). 
  - n'afficher que les trames concernant un protocole particulier : bootp, tcp, icmp,etc 
  
  ![cs31](https://user-images.githubusercontent.com/85891554/146661929-ee796fa2-45f5-47c6-af0a-e5fda84290ed.png)
  ![cs32](https://user-images.githubusercontent.com/85891554/146661930-141b95e8-b879-4f06-a3ec-24bfda914d40.png)
  ![cs](https://user-images.githubusercontent.com/85891554/146661932-6d7fee0a-4437-40e3-9ef0-03bd25bb40c2.png)
  ![cs33](https://user-images.githubusercontent.com/85891554/146661934-85f411ff-bd85-47dc-a7c3-5dcc767e8d40.png)
  
  - n'afficher que les trames dont l'adresse MAC destination est celle de votre machine 
  
  ![cs41](https://user-images.githubusercontent.com/85891554/146661971-bdfcddb9-2b64-451c-9ab2-b111de4c01aa.png)
  
  - n'afficher que les trames échangé entre deux machines d'adresse @IP1 et @IP2 
  
  ![cs42](https://user-images.githubusercontent.com/85891554/146661975-6bd4c92b-2ade-44ce-b37e-4480f0bc012e.png)

