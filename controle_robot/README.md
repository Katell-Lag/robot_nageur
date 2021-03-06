# Robot nageur

## Electronique 

Le choix de l'électronique de ce robot n'est pas encore faite. En effet, nous sommes actuellement capable de réaliser le mouvement et de commander le robot via la BBB cependant elle ne permet par de réaliser une boucle fermée. La difficulté de ce robot se retrouve dans son mouvement. En effet, réaliser une nage crawlée nécessite une adaptation de la force appliquée suivant l’environnement (eau ou aire). La force appliquée sous l’eau est bien plus importante qu’en dehors si l’on souhaite obtenir une trajectoire et un mouvement constant. Pour cela il faut donc utiliser un système de commande en boucle fermée, et pour cela nous avons donc du étudier les cartes trinamic qui elles réalisent quasi-automatiquement cette boucle fermée.

Afin de réaliser notre robot il nous a fallut étudier comment le contrôler et comment le commander.
Ainsi nous avons donc approximer notre système à ce schéma bloc :

![schéma bloc](https://github.com/Katell-Lag/robot_nageur/blob/main/controle_robot/sch%C3%A9ma_bloc.png?raw=true)

Ce type de système en boucle fermée nous permettra, grâce aux mesures effectuées par nos codeurs et IMU d’ajuster la commande envoyée à notre robot pour lui permettre d’effectuer un mouvement plus fluide, plus juste et de vérifier les positions au cours du temps. La commande envisagée est donc appelée « commande hybride couple-position ».

## Controle des moteurs du robot nageur

Deux solutions ont été abordées: 
  - Avec une BeagleBone Blue reliée aux moteurs par des ESC. Nous arrivons à contrôler les moteurs en boucle ouverte grâce aux encodeurs, et ainsi à reproduire le mouvement de crawl d'un bras. Nous avons également essayé le retour en boucle fermé
  - Avec une Trinamic, qui contrôle toute seule en boucle fermée avec davantage de précision
