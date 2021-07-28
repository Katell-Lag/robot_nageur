# Robot_nageur
Ce dépôt rassemble les codes et les documents réalisés lors du stage ingénieur d'Anna Agobian et Katell Lagattu.

Vous pourrez retrouver l'ensemble des scripts python et C, les fichiers des pièces 3D, datasheet et documentations utilisées.

Un README a été créé pour chacun des dossiers afin d'ajouter une description plus détaillée des documents disponibles.

## Décomposition du robot 

Ce robot se compose de la manière suivante : un buste (stockant l’ensemble du matériel électronique : cartes, batteries etc.) composé de 2 bras, équipé chacun de 3 articulations (une épaule, une rotation biceps et un coude), et de 2 jambes, équipée chacune d’un unique moteur. 

Au total, le robot sera composé de 9 tubes étanches (3 pour chaque bras, 1 pour le buste et 1 pour chaque jambe), d’une dizaine de cartes électroniques, d’une unique batterie. Parmi les cartes électroniques on retrouvera soit une unique BeagleBone Blue accompagnée de 3 ESC pour générer le signal PWM de nos BLDC, soit une raspberry PI3 (ou plusieurs suivant les SPI disponibles) accompagnée de 3 cartes (1pour chaque moteur du bras) trinamic TMC4671+TMC6100-BOB pour réaliser la boucle fermée et générer le signal PWM des BLDC. 
En plus de cela sera rajouté des IMU (centrales inertielles) aux biceps, avant-bras et jambes afin de s’assurer du mouvement exécuté. Elles seront alors accompagnées d’une carte STM32 permettant de traiter leurs données et de les communiquer à la carte mère.

## Aspect général du robot

Réaliser ce robot doit être fait en diverses étapes très distinctes. En effet, avant de partir sur sa construction et le tester dans l'eau il faut vérifier son mouvement, gérer l'emmêlement des fils électriques etc.
Ainsi nous avions donc défini cet aspect global de réalisation :

![aspect général](https://github.com/Katell-Lag/robot_nageur/blob/main/controle_robot/architecture_globale.jpg?raw=true)

Nous avons donc actuellement réaliser le bras gauche, simuler le bras, le robot entier en virtuel et réaliser le bouton d'urgence. Nous en étions à la réalisation du bras gauche en réel.

Pour tout renseignement supplémentaire contactez nous via les emails suivants :
##### anna.agobian@etu.umontpellier.fr
##### katell.lagattu@ensta-bretagne.org
