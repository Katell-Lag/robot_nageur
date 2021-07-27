# CONTROLE DES TROIS MOTEURS EN BOUCLE OUVERTE AVEC LA BEAGLEBONE BLUE

La carte BeagleBone Blue (BBBlue) est une carte de développement open source fonctionnant sous linux.
Disposant de divers modules et interfaces (UART,SPI, IMU, Bluetooth) nécessaires pour notre utilisation et de connecteurs moteurs, cette carte est idéale pour la commande de nos moteurs.

 
Ce dossier contient le code et les makefile nécessaires pour faire fonctionner les trois moteurs (moteur épaule et les 2 moteurs du bras) en boucle ouverte, à l'aide des encodeurs du moteur épaule (encodeur 4) et du moteur 1 (encodeur 1). Nous appelons moteur 1 le moteur relié au channel 1. C'est le moteur dont l'axe est le plus bas.
A l'exécution du code, les trois moteurs simulent la trajectoire de crowl d'un bras. 
NOTE: Nous ne l'avons fait fonctionné que sur table, car on rencontre des soucis de jeux entre les dents des engrenages.

ENVIRONNEMENT:

L'image de la BeagleBone est debian et la librairie utilisée est librobotcontrol.
La Beaglebone sur laquelle nous avons réalisé les tests est la BeagleBone-BB35. Pour se connecter: 
ip: 192.168.8.1
utilisateur: debian
mdp: temppwd



BRANCHEMENTS: voir schéma ARCHI_BBLUE.png



EXECUTION DU CODE:

Le code fonctionnel est: librobotcontrol-1.0.4/examples/codes_tests/rc_moteurs_synchros.c
Pour l'exécuter: se placer dans librobotcontrol-1.0.4/examples puis "make install".
Ensuite revenir dans codes_tests et entrer:
rc_moteurs_synchros -c 3 -a -250000 -f 400 -s 1.0 -m 1400,1600



EXPLICATIONS DE LA COMMANDE: 

Le -c 3 correspond au channel du moteur épaule. Il faut donc bien le brancher sur ce channel. Le -m 1400,1600 correspond à la plage du pwm. Si on veut faire tourner le moteur plus ou moins vite il faut agrandir ou réduire cette plage centrée en 1500. Le -s correspond au switch mode (celui que l'on utilise). Les autres paramètres sont des paramètres par défault.



EXPLICATIONS DU CODE:

Le contrôle se fait grâce aux valeurs des encodeurs (voir commentaires du code dans le switch mode).

CONTROLE EN BOUCLE FERMEE

Le code associé est librobotcontrol-1.0.4/examples/src/rc_moteurs_tour_entier_fonctionne.c
Il s'agit d'un contrôle en vitesse. La variable "val" utilisée dans le SWEEP Mode est la valeur qui régule l'intervalle PWM de façon à avoir des différences de valeurs d'encodeur constantes. En effet, l'erreur correspond à ((valeur_actuelle_encodeur - valeur_ancienne_encodeur) - (valeur_de_reference)).
