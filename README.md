# GENERATEUR

## MODE D'EMPLOI

GENERATEUR est un programme que j'ai avant tout créé pour mon utilisation personnelle. Il est un peu "fouilli", car je n'avais pas initialement prévu de le partager. Un mode d'emploi est donc nécessaire !

Le programme transforme l'ordinateur en improvisateur de musique. Mais ce dernier n'improvise qu'en suivant les directives générales donnees par un musicien. Jouer avec ce programme revient à dire à l'ordinateur qui improvise : "Va plus vite", "module en la mineur", "joue dans les aigus", "joue plus de notes", "maintenant moins de notes", "plus chaotique !", "plus carré rythmiquement", "plus libre rythmiquement", etc. 

Les éléments UI permettant cela sont marqués par des commentaires sur canevas jaune au sein des patchs. Ils sont composés d'un moyen de contrôle à la souris (bouton, interrupteur, slider...) et d'un objet "ctlin" pour utiliser un éventuel contrôleur MIDI externe. Pour faire correspondre les contrôles avec votre matériel MIDI, il suffit de changer l'argument des "ctlin" avec les numéros de MIDI CC que vous utilisez sur votre contrôleur. 

IMPORTANT : 
Le programme ne génère aucun son. Il ne génère que des données MIDI. Il faut donc paramétrer la sortie MIDI de Pure Data pour l'envoyer à l'appareil MIDI de votre choix.


## DESCRIPTION PATCH PAR PATCH


generateur.pd : Patch principal ouvrant le programme.
     - L'interrupteur "START" est un bouton on/off. 
     - La variable "CANAL MIDI" permet de sélectionner le canal MIDI de sortie. Si vous n'y touchez pas, le canal MIDI sera le 1 (même si le nombre affiche 0).


tempo.pd : Ce patch génère deux métronomes. Le premier est le "TEMPO", c'est-à-dire la pulse générale. Le second est la "RESOLUTION", c'est-à-dire la division rythmique maximum de cette pulse initiale. 
     - Le slider "TEMPO" permet de contrôler la vitesse de la pulse générale. 
     - Les boutons horizontaux "RESOLUTION" permettent de sélectionner la division maximum de cette pulse. NB : seules des divisions binaires sont disponibles pour le moment.
     ATTENTION : sur ce patch, la polarité des sliders est inversée. Il faut baisser les sliders pour accélérer le tempo ou augmenter les divisions.


freqnotes.pd : Ce patch filtre les impulses issues de la division max. 
     - Le slider "FREQUENCE" permet de définir, à partir des impulsions des métronomes, la densité de notes qui seront effectivement jouées.


rythmes_intensites.pd : 
     - Slider "POURCENTAGE ALEATOIRE RYTHME" : Lorsque cette valeur est au plus bas, les notes seront toutes jouées au rythme de la pulse générale. Lorsque cette valeur est au plus haut, les notes seront toutes jouées sur des divisions de la pulse (contre-temps). Les intensités sont aléatoires, mais seront globalement plus fortes sur la pulse generale.


modes2.pd :
     - Chaque bouton permet de déterminer le mode avec lequel le programme jouera. Sont disponibles les 7 modes traditionnels, les 7 modes de Messiaen, le "mode" dodécaphonique, et un mode "CUSTOM" avec des listes vides permettant de créer sa propre échelle. Les modes sont constitués de deux listes de chiffres MIDI : à gauche, une liste des hauteurs constituant le mode, et à droite, une liste des notes pôles de ce mode.
     - Le slider "FONDAMENTALE" permet de choisir la note fondamentale sur laquelle sera construite l'échelle du mode. 


notesnew.pd : Ce patch décide des notes qui seront jouées. 
     - Le slider "TESSITURE" fixe la note la plus grave de l'ambitus.
     - Le slider "AMBITUS" détermine l'amplitude de l'ambitus, en partant de la note la plus grave définie par TESSITURE".
     - Le slider "% ALEATOIRE" détermine le pourcentage d'aléatoire des notes. Concrètement, il détermine si une note doit être choisie au hasard dans l'ambitus, ou déterminee par la moyenne des 4 dernières notes jouées. 


durees.pd : Ce patch fonctionne de manière équivalente à notesnew, mais décide de la durée pendant laquelle les notes sont tenues.
     - Le slider "DUREE MINIMUM" fixe la durée la plus courte possible
     - Le slider "DUREE MAXIMUM" fixe la durée la plus longue possible
     - Le slider "% ALEATOIRE" détermine le pourcentage d'aléatoire des durées. Concrètement, il détermine si une durée doit être choisie au hasard entre "DUREE MIN" et "DUREE MAX", ou déterminée par la moyenne des 4 dernières durées. 


freqnotes2.pd, rythme_intensites2.pd, notesnew2.pd, durees2.pd sont des copies et fonctionnent exactement de la même manière que leurs homologues. La seule différence est que la liste envoyée par modes2.pd à notesnew2.pd sera constituée uniquement des notes pôles du mode choisi, alors que notesnew.pd est nourri par l'échelle complète du mode. Cela permet de générer deux "voix" : la première aura un rôle plutôt mélodique, et la seconde un rôle plutôt harmonique. 


Have fun!

Benjamin Bouvrot (alias Doedelzak)
