UTILISATION DE LA TMC6100-EVAL-KIT (VIA TMCL-IDE ET RASPBERRY PI3).

TMCL-IDE:

On accède au TMCL-IDE via usb.
Branchements: voir schéma
Pour faire tourner un des moteurs BLDC: aller dans Wizards et entrer les paramètres visibles dans les captures d'écran du dossier robot_nageur/controle_robot/Trinamic/TMC6100-EVAL-KIT/Setup

Manual : https://www.trinamic.com/fileadmin/assets/Support/Software/TMCL_reference.pdf
Tuto de Trinamic: https://blog.trinamic.com/2020/02/25/driving-a-linear-stage-with-the-tmc4671/


LIEN GITHUB VERS LE CODE PYTHON:

Ce code fonctionne avec une connexion usb, soit entre la Trinamic et un PC, soit entre la Trinamic et une Raspberry.

https://github.com/trinamic/PyTrinamic/blob/master/PyTrinamic/examples/evalboards/TMC4671/TMC4671_eval_BLDC_open_loop.py
