# UTILISATION DE LA TMC4671+TMC6100-BOB

### Ce dossier décrit nos tests pour faire fonctionner le bus SPI entre Raspberry et Trinamic.

REMARQUE PRELIMINAIRE:

Pour accéder à la Raspberry que nous avons utilisée, et qui contient tous nos fichiers tests:

Via un écran, aller dans /etc/wpa_supplicant/wpa_supplicant.conf et rentrer un réseau wifi et son mot de passe pour se connecter via ssh. 

user: pi

mdp: raspberry

BRANCHEMENTS: voir schéma.

CONTEXTE:

Pour contrôler les moteurs avec la TMC4671+TMC6100-BOB, il faut d'une part envoyer les bons registres à la carte, et d'autre part configurer correctement la communication SPI.

REGISTRES:

Les registres que nous avons utilisés sont: 
  - Ceux que nous avons exporté du TMCL-IDE (voir https://github.com/Katell-Lag/robot_nageur/blob/main/controle_robot/Trinamic/TMC6100-EVAL-KIT/20210706_10.24.59_TMC4671-EVAL_Settings_V1.c)
  - Ceux qui sont dans le Pytrinamic et qui fonctionnaient via USB (voir https://github.com/trinamic/PyTrinamic/blob/master/PyTrinamic/examples/evalboards/TMC4671/TMC4671_eval_BLDC_open_loop.py)
 

COMMUNICATION SPI:

Voir TMCAPI_EXAMPLE et TMCAPIEXAMPLE2.

AUTRES METHODES:

Nous avons aussi utilisé d'autres méthodes qui n'ont pas fonctionné non plus, peut-être parce que les cartes utilisées dans ses librairies ne sont pas les mêmes: voir test_levref (à partir de https://github.com/trinamic/PyTrinamic/commit/4e6927a0448545c5d8767285cda3d14c63dbb35c) et tripipy (à partir de https://github.com/pootle/tripipy). 
