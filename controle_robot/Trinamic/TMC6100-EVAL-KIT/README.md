# UTILISATION DE LA TMC6100-EVAL-KIT (VIA TMCL-IDE ET RASPBERRY PI3).

TMCL-IDE:

On accède au TMCL-IDE via usb.

Branchements: voir schéma

Pour faire tourner un des moteurs BLDC: aller dans Wizards et entrer les paramètres visibles dans les captures d'écran du dossier robot_nageur/controle_robot/Trinamic/TMC6100-EVAL-KIT/Setup

Manual : https://www.trinamic.com/fileadmin/assets/Support/Software/TMCL_reference.pdf

Tuto de Trinamic: https://blog.trinamic.com/2020/02/25/driving-a-linear-stage-with-the-tmc4671/


LIEN GITHUB VERS CODE PYTHON FONCTIONNEL:

Ce code fonctionne avec une connexion usb, soit entre la Trinamic et un PC, soit entre la Trinamic et une Raspberry.

https://github.com/trinamic/PyTrinamic/blob/master/PyTrinamic/examples/evalboards/TMC4671/TMC4671_eval_BLDC_open_loop.py

NOTES:

- Si le voyant rouge de la carte s'allume, double cliquer sur Landunsbruecke puis decocher et recocher "enable drivers". Pour éviter qu'il s'allume, il faut decocher cette case avant d'alimenter les moteurs, puis la recocher.
- Nous avons essayé de changer directement le firmware en suivant le tuto: https://blog.trinamic.com/2020/02/28/driving-a-linear-stage-with-the-tmc4671-firmware-adaptation/ mais cela a fait planté la carte. Si jamais cela arrive, court-circuiter id_clk et id_ch0, et redémarrer. On peut alors remettre l'ancien firmware disponible sur le site de Trinamic.
- Le "direct mode" qui permet de contrôler le moteur sans passer par le Wizard fonctionne: https://blog.trinamic.com/2020/02/26/driving-a-linear-stage-with-the-tmc4671-controller-tuning/
