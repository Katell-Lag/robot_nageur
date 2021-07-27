# SIMULATION V-REP

### SIMULATION DE L'ARCHITECTURE

L’architecture du robot créé sous V-REP est celle du vrai robot : un buste, deux bras, deux jambes. 

Les articulations sont modélisées par des joints cylindriques et les parties mécaniques par des cylindres. Le buste est fixe et modélisé par un pavé droit. C’est la première pièce dans l’arbre des dépendances.


### COMMANDE EN POSITION  

Les 8 moteurs (3 par bras et 2 pour les jambes) doivent être commandés en position. Nous avons récupéré le tableau de valeurs de l’ancien groupe, qui correspond aux angles que doivent atteindre chaque pivot à chaque instant. Ce sont donc les différents objectifs que les objets doivent atteindre. 

Le programme a été fait en Lua. Avec la fonction sim.setJointTargetPosition de V-REP et en adaptant les unités et les repères, les 6 moteurs ont pu être commandés en position grâce au tableau de valeurs (voir le child script associé).

La commande se fait de cette manière: lorsque les objets ont atteint l'orientation objectif qui correspond à une valeur du tableau, l'objectif change et devient égal à la prochaine valeur du tableau.

La synchronisation des deux bras se fait avec un décalage d'indices: les deux bras parcourent de manière décalée le même tableau de valeurs.

Nous avons également voulu simuler le milieu aqueux sous V-REP en ajoutant des frottements avec la fonction sim.addForceAndTorque lorsque le bras était censé être dans l’eau. Nous avons également testé différents paramètres comme la densité des pièces. La réaction du bras sous V-REP était alors imprévisible et peu réaliste, et nous avons laissé cette piste de côté.

### Coder sous V-REP

Nos codes se situent au niveau des "primitives" (ou objets) de V-REP. Pour les voir, double-cliquer sur l'icône à côté des noms des objets dans l'arbre des dépendances.

Pour coder sous V-REP directement en Lua, il faut se placer sur la "primitive" à commander, puis cliquer sur Add -> Associated Child Script -> Non Threaded.
