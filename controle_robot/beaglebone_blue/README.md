# CONTROLE DES TROIS MOTEURS EN BOUCLE OUVERTE AVEC LA BEAGLEBONE BLUE

La carte BeagleBone Blue (BBBlue) est une carte de développement open source fonctionnant sous linux.
Disposant de divers modules et interfaces (UART,SPI, IMU, Bluetooth) nécessaires pour notre utilisation et de connecteurs moteurs, cette carte est idéale pour la commande de nos moteurs.

L’un des nombreux avantages de cette carte est que l’on peut accéder à son contenu (codes, exécutables…) via WIFI. On parle de liaison SSH. Cette liaison permet d’ouvrir une session interactive entre une machine distante et le client. Soit nous et la BBBlue (son environnement linux). Ainsi il nous est donc possible de modifier une commande sans démonter le système électronique.

La BBBlue possède dès son utilisation tout une architecture linux. Elle possède également divers exemples de code suivant les modules utilisés, des configurations de GPIO ou autre. C’est donc avec l’appui de ces divers exemples que nous avons implémenté un code permettant de commander les 3 robots. 

## Notre utilisation de la BBBlue

Ainsi disposant de 8 connecteurs moteurs et 4 pour les encodeurs, nous avons choisi de commander 3 moteurs Brushless contrôler par 2 encodeurs avec une unique BBBlue.
Il sera donc nécessaire de disposer de 2 BBBlue pour commander l’ensemble des moteurs.
Ce dossier contient donc le code et les makefile nécessaires pour faire fonctionner les trois moteurs (moteur épaule et les 2 moteurs du bras) en boucle ouverte, à l'aide des encodeurs du moteur épaule (encodeur 4) et du moteur 1 (encodeur 1). Nous appelons moteur 1 le moteur relié au channel 1-c'est le moteur dont l'axe est le plus bas-.
A l'exécution du code, les trois moteurs simulent la trajectoire de crowl d'un bras. 

###### NOTE: Nous ne l'avons fait fonctionné que sur table, car on rencontre des soucis de jeux entre les dents des engrenages.

## Architecture 
Ainsi l’architecture envisagée pour la structure finale du système serait la suivante :

![architecture générale](https://github.com/Katell-Lag/robot_nageur/blob/main/controle_robot/beaglebone_blue/archi_generale.jpg?raw=true)

c : type de connexion
p : nombre de ports/fils envisagés

## Environnement :

L'image de la BeagleBone est debian et la librairie utilisée est librobotcontrol.
La Beaglebone sur laquelle nous avons réalisé les tests est la BeagleBone-BB35. Pour accéder à son contenu, il faut se connecter en WIFI à celle-ci puis en SSH(Putty, WinSCP ...) avec les parmètres suivant : 
###### ip: 192.168.8.1
###### utilisateur: debian
###### mdp: temppwd

## Branchements : 

*voir schéma ARCHI_BBLUE.png*
![architecture BBB](https://github.com/Katell-Lag/robot_nageur/blob/main/controle_robot/beaglebone_blue/ARCHI_BBBlue.PNG?raw=true)

## Exécution de code :

Vous trouverez dans le dossier *librobotcontrol-1.0.4/examples* plusieurs codes réalisant diverses commandes.  
Le code fonctionnel est: librobotcontrol-1.0.4/examples/codes_tests/rc_moteurs_synchros.c
Pour l'exécuter il faut se placer dans le dossier *librobotcontrol-1.0.4/examples*, réaliser un "*make*" afin de créer l'exécutable du fichier de commande rc_moteurs_synchros.c.
Ainsi le fichier exécutable est créé dans le dossier codes_tests et pour lancer l'exécution la commande à appliquer est la suivante :
##### rc_moteurs_synchros -c 3 -a -250000 -f 400 -s 1.0 -m 1400,1600

### Commande

Le -c 3 correspond au channel du moteur épaule. Il faut donc bien le brancher sur ce channel. Le -m 1400,1600 correspond à la plage du pwm. Si on veut faire tourner le moteur plus ou moins vite il faut agrandir ou réduire cette plage centrée en 1500. Le -s correspond au switch mode (celui que l'on utilise). Les autres paramètres sont des paramètres par défault.

### Explications du code

Le contrôle se fait grâce aux valeurs des encodeurs (voir commentaires du code dans le switch mode).
La première rotation du mouvement se fait avec les deux moteurs tournant dans le sens opposé, et le second mouvement uniquement avec le moteur 1.
Il faut faire attention au sens de comptage des encodeurs qui peut être négatif (voir code).

CONTROLE EN BOUCLE FERMEE

Le code associé est librobotcontrol-1.0.4/examples/src/rc_moteurs_tour_entier_fonctionne.c
Il s'agit d'un contrôle en vitesse. La variable "val" utilisée dans le SWEEP Mode est la valeur qui régule l'intervalle PWM de façon à avoir des différences de valeurs d'encodeur constantes. En effet, l'erreur correspond à ((valeur_actuelle_encodeur - valeur_ancienne_encodeur) - (valeur_de_reference)).
