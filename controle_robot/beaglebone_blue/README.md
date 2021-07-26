CONTROLE DES TROIS MOTEURS EN BOUCLE OUVERTE AVEC LA BEAGLEBONE BLUE

Ce dossier contient le code et les makefile nécessaires pour faire fonctionner les trois moteurs (moteur épaule et les 2 moteurs du bras) en boucle ouverte, à l'aide des encodeurs du moteur épaule et du moteur 1. Nous appelons moteur 1 le moteur relié au channel 1 et dont l'encodeur est également branché sur le 1. C'est le moteur dont l'axe est le plus bas.
A l'exécution du code, les trois moteurs simulent la trajectoire de crowl d'un bras. 
NOTE: Nous ne l'avons fait fonctionné que sur table, car on rencontre des soucis de jeux entre les dents des engrenages.

ENVIRONNEMENT:

L'image de la BeagleBone est debian et la librairie utilisée est librobotcontrol.
La Beaglebone sur laquelle nous avons réalisé les tests est la BeagleBone-BB35. Pour se connecter: 
ip: 192.168.8.1
utilisateur: debian
mdp: temppwd



BRANCHEMENTS: voir schéma



EXECUTION DU CODE:

Le code fonctionnel est: librobotcontrol-1.0.4/examples/codes_tests/rc_moteurs_synchros.c
Pour l'exécuter: se placer dans librobotcontrol-1.0.4/examples puis "make install".
Ensuite revenir dans codes_tests et entrer:
rc_moteurs_synchros -c 3 -a -250000 -f 400 -s 1.0 -m 1400,1600



EXPLICATIONS DE LA COMMANDE: 

Le -c 3 correspond au channel du moteur épaule. Il faut donc bien le brancher sur ce channel. Le -m 1400,1600 correspond à la plage du pwm. Si on veut faire tourner le moteur plus ou moins vite il faut agrandir ou réduire cette plage centrée en 1500. Les autres paramètres sont des paramètres par défault.
