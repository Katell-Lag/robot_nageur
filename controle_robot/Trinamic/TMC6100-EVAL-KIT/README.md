# UTILISATION DE LA TMC6100-EVAL-KIT (VIA TMCL-IDE ET CODE PYTHON).

## PRESENTATION:

La TMC6100-EVAL-KIT est composée d'un microcontrôleur Landungsbrücke, deux cartes de liaisons Eselsbrücke, une carte "motion controller" TMC4671-EVAL et une carte driver TMC6100-EVAL. L'intérêt d'utiliser une telle carte par rapport à une BeagleBone est qu'elle est capable de contrôler un moteur BLDC en boucle fermée, aussi bien en couple qu'en position.

## TMCL-IDE:

On accède au TMCL-IDE via usb. Il se télécharge à partir du lien suivant : https://www.trinamic.com/support/software/tmcl-ide/ 

Cet IDE a été conçu par TRINAMIC afin de simuler à partir d'une fenêtre "*wizard*" le comportement du moteur en sortie. En effet, il permet de visualiser en direct le comportement du BLDC en fonction des encodeurs, ou "sensors hall", de modifier les paramètres PI du correcteur et également ceux du moteur lui-même. Il est également possible de changer le firmware de la Landungsbrücke afin d'y entrer par défault les paramètres souhaités. Cependant, nous n'avons actuellement pas réussi à réaliser cette action correctement.

*EXEMPLE : Pour faire tourner un des moteurs BLDC: aller dans Wizards et entrer les paramètres visibles dans les captures d'écran du dossier robot_nageur/controle_robot/Trinamic/TMC6100-EVAL-KIT/Setup
La boucle fermée fonctionne, ainsi que le FOC (Field Oriented Control).* 

## BRANCHEMENTS: 

voir schéma
![branchement usb](https://github.com/Katell-Lag/robot_nageur/blob/main/controle_robot/Trinamic/TMC6100-EVAL-KIT/ARCHI_usb.PNG?raw=true)


## DOCUMENTS UTILES

* Manual : https://www.trinamic.com/fileadmin/assets/Support/Software/TMCL_reference.pdf

* Tuto de Trinamic pour la configuration Wizard: https://blog.trinamic.com/2020/02/25/driving-a-linear-stage-with-the-tmc4671/

* Tuto en vidéo de la configuration Wizard: https://www.youtube.com/watch?v=g2BHEdvW9bU&t=32s


## LIEN GITHUB VERS CODE PYTHON FONCTIONNEL:

Sans passer par l'IDE mais en exécutant un code python avec une liaison USB, nous arrivons à faire tourner le moteur en boucle ouverte.
Ce code fonctionne avec une connexion usb, soit entre la Trinamic et un PC, soit entre la Trinamic et une Raspberry.

https://github.com/trinamic/PyTrinamic/blob/master/PyTrinamic/examples/evalboards/TMC4671/TMC4671_eval_BLDC_open_loop.py

###### NOTES:

- Si le voyant rouge de la carte s'allume, double cliquer sur Landunsbruecke puis décocher et recocher "enable drivers". Pour éviter qu'il s'allume, il faut décocher cette case avant d'alimenter les moteurs, puis la recocher.
- Nous avons essayé de changer directement le firmware en suivant le tuto: https://blog.trinamic.com/2020/02/28/driving-a-linear-stage-with-the-tmc4671-firmware-adaptation/ mais cela a fait planter la carte. Si jamais cela arrive, il suffit de court-circuiter id_clk et id_ch0, puis de redémarrer/rebrancher la carte. On peut alors remettre l'ancien firmware disponible sur le site de Trinamic.
- Le "direct mode" qui permet de contrôler le moteur sans passer par le Wizard fonctionne: https://blog.trinamic.com/2020/02/26/driving-a-linear-stage-with-the-tmc4671-controller-tuning/
