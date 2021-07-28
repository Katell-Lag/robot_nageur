# Robot nageur

## Décomposition du robot 

Ce robot se compose de la manière suivante : un buste (stockant l’ensemble du matériel électronique : cartes, batteries etc.) composé de 2 bras, équipé chacun de 3 articulations (une épaule, une rotation biceps et un coude), et de 2 jambes, équipée chacune d’un unique moteur. 

Au total, le robot sera composé de 9 tubes étanches (3 pour chaque bras, 1 pour le buste et 1 pour chaque jambe), d’une dizaine de cartes électroniques, d’une unique batterie. Parmi les cartes électroniques on retrouvera soit une unique BeagleBone Blue accompagnée de 3 ESC pour générer le signal PWM de nos BLDC, soit une raspberry PI3 (ou plusieurs suivant les SPI disponibles) accompagnée de 3 cartes (1pour chaque moteur du bras) trinamic TMC4671+TMC6100-BOB pour réaliser la boucle fermée et générer le signal PWM des BLDC. 
En plus de cela sera rajouté des IMU (centrales inertielles) aux biceps, avant-bras et jambes afin de s’assurer du mouvement exécuté. Elles seront alors accompagnées d’une carte STM32 permettant de traiter leurs données et de les communiquer à la carte mère.

Une tête, créée durant un stage ultérieur, sera également présente sur le robot final afin de lui indiquer la direction à suivre et de le faire nager entre diverses bouées marines.

De plus, suivant le poids du robot et sa flotta, il sera peut-être nécessaire d’y ajouter du volume, autrement dit des bouées, afin d’assurer sa flottabilité.

## Electronique 

Le choix de l'électronique de ce robot n'est pas encore faite. En effet, nous sommes actuellement capable de réaliser le mouvement et de commander le robot via la BBB cependant elle ne permet par de réaliser une boucle fermée. La difficulté de ce robot se retrouve dans son mouvement. En effet, réaliser une nage crawlée nécessite une adaptation de la force appliquée suivant l’environnement (eau ou aire). La force appliquée sous l’eau est bien plus importante qu’en dehors si l’on souhaite obtenir une trajectoire et un mouvement constant. Pour cela il faut donc utiliser un système de commande en boucle fermée, et pour cela nous avons donc du étudier les cartes trinamic qui elles réalisent quasi-automatiquement cette boucle fermée.

Afin de réaliser notre robot il nous a fallut étudier comment le contrôler et comment le commander.
Ainsi nous avons donc approximer notre système à ce schéma bloc :

![schéma bloc](https://github.com/Katell-Lag/robot_nageur/blob/main/controle_robot/sch%C3%A9ma_bloc.png?raw=true)

Ce type de système en boucle fermée nous permettra, grâce aux mesures effectuées par nos codeurs et IMU d’ajuster la commande envoyée à notre robot pour lui permettre d’effectuer un mouvement plus fluide, plus juste et de vérifier les positions au cours du temps. La commande envisagée est donc appelée « commande hybride couple-position ».

# CONTROLE DES MOTEURS DU ROBOT NAGEUR

Deux solutions ont été abordées: 
  - Avec une BeagleBone Blue reliée aux moteurs par des ESC. Nous arrivons à contrôler les moteurs en boucle ouverte grâce aux encodeurs, et ainsi à reproduire le mouvement de crawl d'un bras. Nous avons également essayé le retour en boucle fermé
  - Avec une Trinamic, qui contrôle toute seule en boucle fermée avec davantage de précision
