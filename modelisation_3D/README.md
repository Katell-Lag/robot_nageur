# Modélisation 3D

Dans ce dossier-là, vous disposerez de l'ensemble des pièces créées pour l'épaule de notre robot.
Voici une modélisation correspondant au système étudié lors de notre stage :

![modélisation bras](https://github.com/Katell-Lag/robot_nageur/blob/main/modelisation_3D/Assemblage_bras_Reel.PNG?raw=true)

## Choix de cette conception du bras

Cette conception du bras nous a été imposée par notre tuteur. Elle consiste à réaliser les rotations coudaire et du biceps à partir de la relation entre 2 moteurs de drones (AXI 2217/12 GOLD LINE). En effet, pour réaliser une rotation uniquement coudaire il suffit de n'activer qu'un des moteurs (dans ntore cas le moteur 1) et pour réaliser une rotation du biceps il nécessite d'ajouter l'effort réaliser par les 2 moteurs. Un ajout de réducteur ( système d'engrenage/roues dentées avec rapport de réduction 60:1) a été nécessaire pour obtenir une vitesse réelle de rotation du bras.
Pour ce qui concerne l'épaule, le choix du moteur a été imposé également puisque nous l'avoir récupéré d'un autre projet. Vous pouvez retrouver l'étude de son couple et de ses caratérisque dans le document *Rapport_de projet_robotique* (https://github.com/Katell-Lag/robot_nageur/blob/main/modelisation_3D/Rapport_de%20projet_robotique.pdf) à la partie 4.1.1

## Résultats obtenus

Comme vous pouvez le constater l'inconvénient de cette conception du bras est sa répartition du poids du bras. En fait, 2 des moteurs du bras se trouve au niveau du coude, ainsi tout l'effort créé par les moteurs prend en compte le poids de l'ensemble d'entre eux, et la distance épaule-coude est bien trop grande pour réduire cet effort.
En plus de cela, étant donné que les rotations du coude et du biceps se réaliser après réduction des moteurs -réaliser par un système d'engrenage/roues dentées (réduction 60:1)-, le poids, les minimes imprécisions de mesures etc. ne permettent pas de réaliser le mouvement correctement. C'est-à-dire que certaines dents des roues dentées peuvent sauter ou riper, un accou important lors de la descente du bras se réalise etc.

Ce prototype malgré ses nombreux défauts, nous a été très utile, puisqu'il nous a permis de constater que la fixation de l'axe des roues dentées n'était pas suffisante et qu'un deuxième point d'attache est nécessaire. Que l'axe de raccord moteurs-biceps n'était pas assez long. Et qu'il faut rapprocher au plus les moteurs vers l'épaule.


##### Notez que la modélisation a été réalisée sous OnShape un logiciel de conception assistée par ordinateur (CAO) disponible en ligne.
https://www.onshape.com/en/
