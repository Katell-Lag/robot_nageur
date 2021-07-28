# UTILISATION DE LA TMC4671+TMC6100-BOB

La carte  trinamic TMC4671+TMC6100-BOB est une carte de développement permettant à l'utilisateur de prototyper des applications directes à ses moteurs. Cette carte permet de contrôler un moteur, de récupérer les données de 2 encodeurs et surtout de réaliser une boucle fermée. 
En effet, l'avantage principal de ces cartes est leur contrôle en boucle fermée. Ceci permet d'obtenir un système plus performant, plus stable et optimal: le retour des encodeurs permet d'asservir le système via un correcteur PID et d'assurer une stabilité.
Ces cartes permettent aussi de contrôler les moteurs par la commande FOC(Field-Oriented Control)- soit contrôle à flux orienté-. 

### Commande FOC

En effet, cette commande FOC- appelée également "commande vectorielle"- permet de garder une précision continue des commandes envoyées, notamment pour les moteurs BLDC (BrushLess Direct Courant). Pour se faire, c'est à partir de la consigne de vitesse du moteur que le flux et le couple nécessaire sont calculés et qu'ensuite les courants requis sont déduits. 

La commande FOC est composée de deux forces Q (quadrature) et D (direct), perpendiculaire et parallèle à l'axe des pôles du rotor. 

### Synoptique

![image](https://user-images.githubusercontent.com/87979643/127165290-aca9550f-c24e-4490-8e84-b1ce6d385c75.png)

### Ce dossier décrit nos tests pour faire fonctionner le bus SPI entre Raspberry et Trinamic.

#### REMARQUE PRELIMINAIRE:

Pour accéder à la Raspberry que nous avons utilisée, et qui contient tous nos fichiers tests:

Via un écran, aller dans /etc/wpa_supplicant/wpa_supplicant.conf et rentrer un réseau wifi et son mot de passe pour se connecter via ssh. 

user: pi

mdp: raspberry

#### BRANCHEMENTS: 

voir schéma.

![image](https://github.com/Katell-Lag/robot_nageur/blob/main/controle_robot/Trinamic/TMC4671+TMC6100-BOB/ARCHI_pi3.PNG?raw=true)

#### CONTEXTE:

Pour contrôler les moteurs avec la TMC4671+TMC6100-BOB, il faut d'une part envoyer les bons registres à la carte, et d'autre part configurer correctement la communication SPI. Nous n'avons pas réussi à faire fonctionner le SPI, mais ce dossier rassemble nos pistes.

#### REGISTRES:

Les registres que nous avons utilisés sont: 
  - Ceux que nous avons exporté du TMCL-IDE (voir https://github.com/Katell-Lag/robot_nageur/blob/main/controle_robot/Trinamic/TMC6100-EVAL-KIT/20210706_10.24.59_TMC4671-EVAL_Settings_V1.c)
  - Ceux qui sont dans le Pytrinamic et qui fonctionnaient via USB (voir https://github.com/trinamic/PyTrinamic/blob/master/PyTrinamic/examples/evalboards/TMC4671/TMC4671_eval_BLDC_open_loop.py)
 

#### COMMUNICATION SPI:

Voir TMCAPI_EXAMPLE et TMCAPI_EXAMPLE2.

Ces codes sont inspirés du tuto: http://blog.trinamic.com/2018/02/19/stepper-motor-with-tmc5160/

Ce tuto explique comment relier une Raspberry Pi3 à une TMC5160-BOB.

Nous avons essayé d'adapter le code de différentes manières pour faire fonctionner la liaison avec notre carte, mais sans succès.

#### NOTES SUR LA COMMUNICATION SPI:

- Nous utilisons la librairie bcm2835 pour configurer le SPI.

- Nous avons une incertitude sur les modes des PIN (HIGH ou LOW). De plus, la carte du tuto ne possède pas les mêmes PIN que la nôtre. Par exemple, nous avons supposé qu'il ne fallait pas se soucier du CLK.

- Concernant la fonction tmc4671_readwriteByte, elle doit être présente si l'on utilise la dernière version du TMC-API. Nous ne savons pas si elle est nécessaire dans notre cas.

- Les fonctions définies dans le TMC_SPI.c sont les fonctions permettant de transmettre les données en SPI, plus précisément d'écrire dans les registres de la carte via SPI.

- Nous avons essayé de lire des données provenant de la carte avec tmc4671_ReadInt mais sans succès. Il semble que la liaison ne se fasse pas.

- Après avoir réalisé des tests grâce à un loopback test avec l'API spidev, nous avons conclu que le problème n'était pas la Raspberry elle-même: https://www.raspberrypi.org/documentation/hardware/raspberrypi/spi/README.md

- A l'oscilloscope, nous avons également pu observer que des trames étaient bien envoyées de la Raspberry vers la Trinamic. Nous pensons donc que la Trinamic ne parvient pas à interpréter ces trames.

#### AUTRES METHODES:

Nous avons aussi utilisé d'autres méthodes qui n'ont pas fonctionné non plus, peut-être parce que les cartes utilisées dans ses librairies ne sont pas les mêmes: voir test_levref (à partir de https://github.com/trinamic/PyTrinamic/commit/4e6927a0448545c5d8767285cda3d14c63dbb35c) et tripipy (à partir de https://github.com/pootle/tripipy). 
