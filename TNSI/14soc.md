# Système On Chip : SOC

## Petits rappels

Nous avons étudié, en première, l'architecture Van Neuman ainsi que les portes logiques. N'hésitez pas à aller y jeter un coup d'oeil pour raviver vos souvenirs.

Les [transistors](https://fr.wikipedia.org/wiki/Transistor) qui permettent de fabriquer ces portes logiques ont été inventés en 1947. 

![](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5a/Transistors.agr.jpg/800px-Transistors.agr.jpg)

Le premier [circuit intégré](https://fr.wikipedia.org/wiki/Circuit_int%C3%A9gr%C3%A9) date de 1958 et ouvre l'air de l'informatique moderne et l'utilisation du germanium puis du silicium.

## Les composants et la carte mère

### Le CPU

Le [CPU](https://fr.wikipedia.org/wiki/Processeur) (_Central Processing Unit_), c'est à dire le micro-processeur,  qui est responsable de l'exécution des instructions et se fiche sur le support adéquate (le _socket_). 

Le premier microprocesseur date de 1965 : il s'agit déjà d'un _Intel_ : le [4004][https://fr.wikipedia.org/wiki/Intel_4004). c’est-à-dire la première intégration réussie de toutes les fonctions d’un processeur sur 
un seul et unique circuit intégré :

![4004](https://upload.wikimedia.org/wikipedia/commons/thumb/5/55/Intel_C4004.jpg/1024px-Intel_C4004.jpg)

Voici un autre processeur, l' [intel 80486](https://fr.wikipedia.org/wiki/Intel_80486SX) de 1990. Cadencé à ... 25 MHz

![CPU intel](https://upload.wikimedia.org/wikipedia/commons/thumb/c/c5/Intel_i486_sx_25mhz_2007_03_27b.jpg/1024px-Intel_i486_sx_25mhz_2007_03_27b.jpg)

Voici un AMD de la famille des [Rysen](https://fr.wikipedia.org/wiki/Ryzen) en 2017 : le Ryzen 7 cadencé à 2666 MHz.

![ le Rysen, en 2017](https://upload.wikimedia.org/wikipedia/commons/thumb/a/a6/AMD_Ryzen_1800X_DSC_0251.jpg/631px-AMD_Ryzen_1800X!_DSC_0251.jpg)

* Le cœur du CPU bat (travaille) à une certaine fréquence : à chaque période (l'inverse  de la fréquence, qu'on appelle _cycle d'exécution_), le cœur exécute une instruction.

* Le rythme de la loi de Moore, qui prévoit de doubler le nombre de transistore dans nue puce chaque année , commence a avoir du mal à être suivie :
  
  * La finesse de gravure approche des dimensions de l'ordre des atomes, difficile de poursuivre dans cette voie ...
  * La chaleur dissipé par les CPU est le problème majeur qui empêche la poursuite des montée en fréquence.

* POur palier à ce problème, un CPU moderne, possède plusieurs cœur. Chacun d'entre eux peut, si l'OS le demande, exécuter une instruction à chaque cycle. Lorsque plusieurs cœurs travaillent en même temps, on parle d'exécution en parallèle... Encore faut-il que les logiciels soient programmés de façon à en tirer parti !

### La RAM

Les barrettes de mémoire (la [RAM](https://fr.wikipedia.org/wiki/M%C3%A9moire_vive) pour _Random Acces Memory_) qui offrent une zone de stockage des données volatile (non permanente). Elle est toujours vide au démarrage puis le système d'exploitation qui y charge les données dont il a besoin ou les décharge s'ils sont terminés.

![RAM](https://upload.wikimedia.org/wikipedia/commons/thumb/a/a2/Elixir_M2U51264DS8HC3G-5T_20060320.jpg/800px-Elixir_M2U51264DS8HC3G-5T_20060320.jpg)

### Le GPU

La carte graphique, aussi appelée [GPU](https://fr.wikipedia.org/wiki/Processeur_graphique) (_Graphic Processing Unit_) qui s'occupe des calculs nécessaires à l'affichage 2D et 3D.

Elle peut être intégrée à la carte mère, au CPU,  ou proposer son propre _chipset_ .

Voici une précurseur de la 3D dont les gamers rêvaient en 2005 : la Geforce2 et ses 64Mo de mémoire.

![Geforce2](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b1/NVidia_GeForce2_MX400.jpg/800px-NVidia_GeForce2_MX400.jpg)

Plus récente, la Geforce 1030 de 2018, cadencé à 1265 MHz et embarquant 2gb de  mémoire... et nécéssitant un énorme radiateur pour son refroidissement !

![Geforce 1030](https://upload.wikimedia.org/wikipedia/commons/thumb/f/fc/MSI_GeForce_GT_1030_2GH_LP_OC_-_front_and_back_-_2018-05-14.jpg/400px-MSI_GeForce_GT_1030_2GH_LP_OC_-_front_and_back_-_2018-05-14.jpg)

### Le stockage de masse

La mémoire de stockage, aussi appelée mémoire de masse, c'est à dire les disques durs, [SSD](https://fr.wikipedia.org/wiki/SSD), clés USB, carte SD ou autres.

Voici un disque dur à plateau magnétique. Encore utilisé, notamment pour les grosses capacités de plusieurs téraoctets.

![Disuqe dur](https://upload.wikimedia.org/wikipedia/commons/thumb/0/01/Hard_drive-fr.svg/507px-Hard_drive-fr.svg.png)

Quelques mémoires flash :

![mémoire flash](https://upload.wikimedia.org/wikipedia/commons/a/a4/Flash_memory_cards_size.jpg)





### Contrôleurs de communication

Chaque support et protocole de communication nécessite un contrôleur dédié :

* réseau Ethernet

* fibre optique

* Wifi

* Bluetooth

Voici une carte réseau et sa sortie [RJ45](https://fr.wikipedia.org/wiki/RJ45) (rectangulaire, la plus utilisée) et une sortie [10Base2](https://fr.wikipedia.org/wiki/10BASE2) (ronde) :

![carte réseau](https://upload.wikimedia.org/wikipedia/commons/thumb/9/9e/Network_card.jpg/800px-Network_card.jpg)

### Contrôleur audio

Le contrôleur audio, la [carte son](https://fr.wikipedia.org/wiki/Carte_son),  s'occupe .. de l'audio. Si. Il est parfois (souvent) soit intégré à la carte mère soit directement au processeur. Cependant, il existe des cartes spécifiques haut de gamme, pour les mélomanes ou les musiciens, qui, à l'instar des GPU, libère le CPU de la gestion du son.

Ci-dessous, la carte son Onkyo Wavio, en 2007.

![carte son](https://upload.wikimedia.org/wikipedia/commons/thumb/4/49/Onkyo_Wavio_SE-90PCI.jpg/800px-Onkyo_Wavio_SE-90PCI.jpg)

### Autres contrôleurs

Il existe une multitude de contrôleurs comme :

* Celui de l'alimentation (Batterie ...)
* Les capteurs divers (GPS, radio, boussole, accéléromètres, température, empreinte digitale ...)

### Les entrées-sorties (E/S)

Les contrôleurs et interfaces de communication, aussi appelés entrées/sorties (E/S) ou, en anglais, _input/output_ (I/O) sont des composants électroniques destinées à accueillir les différents périphériques qu'utilise l'ordinateur comme une souris, un clavier, un disque dur, les cartes réseaux, la carte graphique, la carte son ...

### Les Bus

Ca sert à quoi un [Bus](https://fr.wikipedia.org/wiki/Bus_de_donn%C3%A9es) ? Et bien à transporter tiens ! A transporter les données d'un composant à l'autre.

Les bus sont l'ensemble des circuits et des protocoles de communication qui gèrent les échanges entre les composants de l'ordinateur qui, grâce à eux, sont inter-connectés.

On pourrait faire une analogie avec le réseau routier (le circuit) qui permet aux véhicules (les données) de circuler en suivant un code de la route (les protocoles) établi selon le type de véhicule.

Les Bus les plus connus sont :

* L'incontournable USB
* Le PCI pour les cartes réseaux, cartes sons, anciennes cartes garphiques.
* Le PCI _express_,  utilisé pour certaines cartes graphiques, la carte son ou la carte réseau.
* l'AGP, le standard pour les cartes graphiques actuelles.

### La carte mère

Dans un ordinateur traditionnel, comme les PC de bureau, une _carte mère_ accueille les différents composants de l'ordinateur. Le circuit qu'elle utilise pour relier tous les composants est appelé _chipset_. Il se divise en deux parties distinctes :

* Le pont nord (_North Bridge_) pour les périphériques rapides.
* le pont sud (_South bridge_) pour les autres.

Voici un petit schéma simple pour représenter cela :

![bus de données](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f7/Motherboard_diagram_fr.svg/370px-Motherboard_diagram_fr.svg.png)

> à découvrir :
> 
> * Le processeur 
> * les barrettes de RAM
> * le disque dur 
> * La carte graphique récente (BUS AGP) 
> * La carte son et la carte réseau (BUS PCI)
> * Port USB 
> * Sortie VGA  
> * Sortie parallèle 
> * Sortie Ethernet 
> * Régulateur de voltage 
> * Pile du BIOS 
> 
> 

La carte mère qui supporte les différents composants comme nous l'avons vu plus présente des avantages mais aussi inconvénients.

Du côté des avantages, on peut citer :

* la facilité à changer de composants
* la possibilité d'_upgrader_ son ordinateur avec des composants meilleurs ou plus récent.
* la possibilité de remplacer un composant qui tombe en panne sans avoir à changer les autres.
* L'espace permettant une bonne ventilation, il est possible de dissiper la chaleur et d'utiliser des composants très puissant en terme de performance.

Du côté des inconvénients, on trouve :

* l'espace nécessaire pour l'ensemble des pièce
* La quantité de câblages nécessaires pour relier les composants entre eux
* la relative lenteur engendrée par la taille des bus et la distance que doivent parcourir les données entre des composants éloignés
* une tension d'alimentation élevée et une consommation énergétique importante
* une dissipation thermique importante par effet Joule 
* les coûts de fabrication et d'industrialisation de tous les composants qu'il faut concevoir séparément.

## Les SoC (System On Chip)

### Qu'est-ce que c'est ?

La poursuite de la performance pure n'est plus la seule course dans laquelle sont engagés les concepteurs. Avec la miniaturisation et les systèmes embarqués et le succès planétaire des smartphones (entre autres),  le gain de place, la consommation (l'autonomie donc), la facilité et le coût de production sont devenus des problèmes de premier plan.

Une solution proposée est d'embarquer tous les composants, ou presque, sur une même puce : c'est le **S**ystem **o**n **C**hip.

Sur une seule puce, on trouve tous les contrôleurs nécessaires à son fonctionnement :

* Le CPU
* le GPU
* La RAM
* les contrôleurs de son et de communication
* Les bus
* Certains capteurs 

Le stockage de masse est souvent confié à une carte SD en attendant de pouvoir également être intégré à la puce.

Il existe plusieurs architecture pour les SoC  : 

* L'architecture [x86](https://fr.wikipedia.org/wiki/X86) d'Intel 

* L'architecture [ARM](https://fr.wikipedia.org/wiki/Architecture_ARM), qui est la plus répandue et que l'on retrouve dans la plupart des systèmes embarqués :
  
  * la téléphonie mobile et les tablettes (SoC [Qualcomm Snapdragon](https://fr.wikipedia.org/wiki/Qualcomm_Snapdragon) par exemple).
  * les microcontrôleurs comme ceux embarqués par les célèbres cartes [Arduino](https://fr.wikipedia.org/wiki/Arduino).
  * les ordinateurs comme les [raspberry Pi](https://fr.wikipedia.org/wiki/Architecture_ARM).

Les SOC progressent également en terme de performance, notamment grâce au gain en vitesse de transports des données, obtenu en réduisant les distances entre les composants. Il commencent à apparaître également dans les ordinateurs portables où la recherche d'autonomie est également cruciale. En 2020, Apple sort le SoC [M1](https://en.wikipedia.org/wiki/Apple_M1) , basé sur une architecture ARM, pour ses MacBook Pro. Ces derniers sont donnés comme les plus performants des MacBook tout en ayant la meilleurs autonomie de leur histoire.

### Microcontrôleurs et ordinateurs

Dans de nombreux systèmes embarqués, des microcontrôleurs se chargent d'effectuer des calculs spécifiques. Par exemple, le régulateur de vitesse d'une voiture utilise des microcontrôleurs qui adaptent le régime moteur en fonction de la vitesse du véhicule.

Le microcontrôleur possède donc un SoC dédié spécifiquement à sa tâche, une quantité de mémoire et une puissance de calcul réduite et une consommation électrique très faible. Ce sont la plupart du temps des composants autonomes qui exécutent un programme unique.

Un ordinateur utilise une architecture  [Van Neuman](../../../premiere_nsi/architecture/microprocesseurs/architecture_van_neuman.md) pour laquelle programmes et données se partagent la même mémoire. Ainsi une tablette ou un smartphone sont des ordinateurs. Pour nos microcontrôleurs ce n'est pas le cas :

* le programme est stocké dans une mémoire dite _morte_, c'est à dire une mémoire qui ne perd pas ses données même lorsque l'alimentation est coupée.
* les données sont stockée dans une mémoire volatile.

Nous avons déjà parlé des architectures x86 et ARM des SoC destinés à des ordinateurs. Les microcontrôleurs sont, eux, souvent basés sur l'architecture [Harvard](https://fr.wikipedia.org/wiki/Architecture_de_type_Harvard#/media/Fichier:Architecture_Harvard.png) pour laquelle le jeu d'instructions du microprocesseur est réduit (c'est le jeu RISC pour _Reduce Instruction Set_) afin de simplifier l'architecture globale et de gagner en efficacité dans leur tâche spécifique.

![Architecture Harvar](https://upload.wikimedia.org/wikipedia/commons/6/69/Architecture_Harvard.png)

### Quelques SoC

Les smartphones utilisent ce type de puce, comme, ci dessous le SoC Exynos du Samsung Galaxy S3

![smartphone](https://upload.wikimedia.org/wikipedia/commons/thumb/c/cc/Samsung-Exynos-4412-Quad_SoC_used_in_I9300.jpg/800px-Samsung-Exynos-4412-Quad_SoC_used_in_I9300.jpg)

Voici le SOC de l'Iphone 11 : 

![Iphone 11](https://upload.wikimedia.org/wikipedia/commons/thumb/c/c0/A13_APL1W85_iPhone11_mlb_820-01523-A.jpg/747px-A13_APL1W85_iPhone11_mlb_820-01523-A.jpg)

Voici la carte du Raspberry Pi 3, un nano-ordinateur. On remarque qu'il n'y a plus les contrôleurs présents sur la carte mère présentée plus haut : ils sont intégrés à la puce. La carte est donc beaucoup mois chargée : 

![Raspbery](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d2/Raspberry_Pi_3_Model_B.JPG/800px-Raspberry_Pi_3_Model_B.JPG)

Pour finir une carte d'un Arduino où on aperçoit le microcontrôleur [Atmel](https://fr.wikipedia.org/wiki/Atmel_AVR) (le parallélépipède rectangle plein de pattes) basé sur l'architecture Harvard :

![arduino](https://upload.wikimedia.org/wikipedia/commons/thumb/1/17/Arduino_Diecimila.jpg/800px-Arduino_Diecimila.jpg)

### En conclusion

Ainsi les Soc :

* sont moins onéreux à produire.
* sont moins gourmand en énergie donc offre une grande autonomie lorsqu'ils sont emnbarqués dans des appareils mobiles.
* permettent de gagner en vitesse en réduisant la taille des bus.
* simplifient le circuits de la carte mère.

Mais ils ne sont pas exempts de défauts :

* Il est impossible d'upgrader le matériel. Il est figé définitivement.
* Si un composant intégré tombe en panne, il est irréparable et inchangeable : le Soc entier est alors hors service. Plus qu'à changé toute la machine ... Pas le top du point de vue écologie ...
* En 2021, même si ils font des progrès en terme de performance, ils n'atteignent pas les sommets des architectures traditionnelles les plus puissantes. 

## Une vidéo pour finir ?

vous pouvez pour compléter votre culture générale aller visionner la passionnante vidéo suivante : 

[Des circuits aux puces](https://www.college-de-france.fr/site/gerard-berry/course-2008-02-01-10h30.htm)

______

Cours de Mieszczak Christophe : [christophe Mieszczak · GitLab](https://framagit.org/tofmzk)



Licence CC BY SA

sources images : 

* [CPU intel - wikipedia, CC BY SA auteur Henry Mühlpfordt](https://commons.wikimedia.org/wiki/File:Intel_i486_sx_25mhz_2007_03_27b.jpg)
* [CPU Rysen, wikipedia, CC BY SA, auteur Michael Wolf](https://commons.wikimedia.org/wiki/File:AMD_Ryzen_1800X_DSC_0251.jpg)
* [RAM, wikipédia, domaine public](https://commons.wikimedia.org/wiki/File:Elixir_M2U51264DS8HC3G-5T_20060320.jpg)
* [Geforce2, wikipédia](https://commons.wikimedia.org/wiki/File:NVidia_GeForce2_MX400.jpg)
* [Geforce 1030, wikipédia CC BY SA, auteur : Bretwa](https://commons.wikimedia.org/wiki/File:MSI_GeForce_GT_1030_2GH_LP_OC_-_front_and_back_-_2018-05-14.jpg)
* [Disque dur, wikipedia, CC BY SA, auteur historicair](https://commons.wikimedia.org/wiki/File:Hard_drive-fr.svg)
* [Mémoires flash, wikipédia CC BY SA auteur Xell](https://commons.wikimedia.org/wiki/File:Flash_memory_cards_size.jpg)
* [Nano SSD,wikipédia, CC BY SA, auteur Arshane88](https://commons.wikimedia.org/wiki/File:Samsung_860_EVOM.2_MB_key.jpg)
* [Carte réseau, wikipédia CC BY SA, auteur Helix84](https://commons.wikimedia.org/wiki/File:Network_card.jpg)
* [Carte son, wikipédia, CC BY SA, auteur Querren](https://commons.wikimedia.org/wiki/File:Onkyo_Wavio_SE-90PCI.jpg)
* [Transistors, wikipedia CC BY SA](https://commons.wikimedia.org/wiki/File:Transistors.agr.jpg)
* [microprocesseur 4004, wikipedia, CC BY SA](https://commons.wikimedia.org/wiki/File:Intel_C4004.jpg)
* [Bus, wikipédia, CC BY SA, auteur Epok13](https://commons.wikimedia.org/wiki/File:Motherboard_diagram_fr.svg)
* [Carte mère flèchée,production à partir de l'image CC BY SA, auteur Darkone sur wikipédia](https://commons.wikimedia.org/wiki/File:ASRock_K7VT4A_Pro_Mainboard.jpg)
* [Harvard, wikipédia, CC BY SA, auteur Luminium](https://commons.wikimedia.org/wiki/File:Architecture_Harvard.png)
* [Soc samsung, wikipédia, CC BY SA auteur Köf3](https://commons.wikimedia.org/wiki/File:Samsung-Exynos-4412-Quad_SoC_used_in_I9300.jpg)
* [SOC A13, wikipédia, CC BY SA auteur Sonic 8400](https://commons.wikimedia.org/wiki/File:Samsung-Exynos-4412-Quad_SoC_used_in_I9300.jpg)
* [Raspberry, wikipédia, CC BY SA, auteur Jose.gil](https://commons.wikimedia.org/wiki/File:Raspberry_Pi_3_Model_B.JPG)
* [Arduino, wikipédia, CC BY SA, auteur Francky47](https://commons.wikimedia.org/wiki/File:Arduino_Diecimila.jpg)
