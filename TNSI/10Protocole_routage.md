---
title: "Architecture matérielle : Protocole de routage"
subtitle: "cours"
Souce: Cécile Ghesquiere

---

|                       |                                                                                         |                                                                                                                                                                                                                                         |
| --------------------- | --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Protocoles de routage | Identifier , suivant le protocole de routage utilisé , la route empruntée par un paquet | En mode débranché, les tables de routage étant données , on se réfère au nombre de sauts (protocole RIP) ou au coût des routes ( protocole OSPF). Le lien avec les algorithmes de recherche de chemin sur un graphe est mis en évidence |

# Concepts fondamentaux (rappels de 1ère)

## Les principaux protocoles d'Internet

> 🎓 on a acquis : Un protocole est un ensemble de caractéristiques sur lesquelles vont s'appuyer deux entités différentes pour rendre possible une action commune.  

Cette vidéo récapitule les concepts et protocoles de base qui régissent la communication sur Internet.  
[Internet](https://www.youtube.com/watch?v=s18KtOLpCg4&ab_channel=pixeesScienceparticipative)  
Compléter le tableau suivant :  

| protocole | nom | rôle |
|:---------:|:---:|:----:|
|           |     |      |
|           |     |      |
|           |     |      |
|           |     |      |

Les paquets échangés ou __datagramme IP__ sont les entités élémentaires qui transitent sur le réseau physique. Ils proviennent du découpage en petits morceaux des données à transmettre (comme des pages web, du courrier électronique ou de vidéos). Ces paquets sont envoyés séparément sur le réseau et l’information initiale est reconstituée quand les paquets arrivent à destination.

## Couches utilisées du modèle OSI

Le __modèle OSI__ est une norme qui préconise comment les ordinateurs devraient communiquer entre eux. Il est découpé en sept morceaux appelés couches, qui ont chacune un rôle défini, comme le montre le tableau ci-dessous :  

|                      |                                                                                                                                                                                                                                                                         |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 7-application        | Point de contact avec les services réseaux.                                                                                                                                                                                                                             |
| 6-présentation       | Elle s’occupe de tout aspect lié à la présentation des données : format, chiffrement, encodage, etc.                                                                                                                                                                    |
| 5-session            | Elle s’occupe de tout aspect lié à la présentation des données : format, chiffrement, encodage, etc.                                                                                                                                                                    |
| 4-transport          | Choix du protocole de transmission et préparation de l’envoi des données. Elle spécifie le numéro de port utilisé par l’application émettrice ainsi que le numéro de port de l’application réceptrice. Elle fragmente les données en plusieurs séquences (ou segments). |
| 3-réseau             | Rôle : interconnecter les réseaux entre eux ; Rôle secondaire : fragmenter les paquets ;  Matériel associé : le __routeur__                                                                                                                                             |
| 2-liaison de données | Rôle : connecte les machines entre elles sur un réseau local ; Rôle secondaire : détecter les erreurs de transmission; Matériel associé : le __switch__, ou commutateur                                                                                                 |
| 1-physique           | Conversion des trames en bits et transmission physique des données sur le média.                                                                                                                                                                                        |

📝 _Remarque_ : Chaque "objet IP" est physiquement connecté à un réseau local de niveau 2 : la communication avec d’autres "objets IP" appartenant au même réseau local se fait directement via le réseau local de niveau 2 par l’intermédiaire d’un "commutateur". En revanche, la communication avec d’autres "objets IP" d’autres réseaux distants se fait via des passerelles de niveau 3 : les routeurs.
C'est pourquoi nous nous concentrerons dans ce cours sur la couche 3.
 Pour en savoir plus : [ici](https://zestedesavoir.com/tutoriels/2789/les-reseaux-de-zero/un-modele-qui-en-tient-une-couche/ils-en-tiennent-une-couche-osi-et-tcp-ip/#1-le-modele-osi-en-douceur)  

# Adressage IP (notation CIDR)

Toutes les machines connectées à Internet possèdent une adresse unique appelée adresse IP qui est utilisée pour :  

* identifier chaque élément dans l'infrastructure  
* réaliser le routage des datagrammes IP dans celle-ci
  Une adresse IPv4 est un identifiant numérique à 32 bits (soit 4 octets), habituellement représentée en notation décimale pointée.  

![ipv4](./img/ipv4.png)  

Ces 4 octets regroupent :

* l’identifiant du réseau local auquel appartient la machine (extrait grâce "masque de sous-réseau" ou "netmask") : les bits à 1 dans le masque représentent la partie réseau de l'adresse IP ;  
* l'identifiant de l'ordinateur à l'intérieur du réseau.

Le __masque de sous-réseau__ se note de deux façons différentes :  

* la notation "classique" qui couple l'adresse IP et son masque de sous-réseau associé.  

![masque classique](./img/masque1.png)

* la notation CIDR avec un slash qui associe également l'adresse IP d'un hôte à son masque de sous-réseau mais on se contente cette fois de spécifier le nombre de bits à 1 en partant de la gauche (bits de poids fort).
  ![masque CIDR](./img/masque2.png)  

Voici le [lien](http://support-fr.org/lbertrand/wp-content/uploads/sites/16/2016/05/Liste-des-masques-de-sous.pdf) entre les deux notations

# Principe du routage IP

## Le routeur

Un réseau informatique est généralement constitué de __clients, de serveurs__ mais également de __routeurs__ : machines dont le rôle est de relayer les paquets dans le réseau afin de les acheminer vers leur destination finale. Il existe deux types de routeurs comme illustré ci-dessous :

![routeurs](./img/routeurs.png)  

Ressemblant à un switch (ou commutateur), un routeur possède __plusieurs ports__ et dispose d'un logiciel interne bien plus sophistiqué qui lui permet de communiquer avec ses routeurs voisins pour l'aider à déterminer les meilleures routes à emprunter pour acheminer ses paquets.  

![routeur](./img/rout_m.png)  

📝 _Remarque_ : Le routeur est un matériel de couche 3 qui relie plusieurs réseaux. Il doit donc avoir __une interface dans chacun des réseaux auquel il est connecté__. C'est donc tout simplement une machine qui a plusieurs interfaces (plusieurs cartes réseaux), chacune reliée à un réseau. Son rôle va être d'aiguiller les paquets reçus entre les différents réseaux. Un ordinateur ayant deux cartes réseau pourra donc être un routeur. Ce qui le différencie d'un simple ordinateur est qu'un routeur accepte de relayer des paquets qui ne sont pas pour lui alors qu'une simple machine les rejettera. Toute machine connectée à un réseau peut donc jouer le rôle de routeur. Il suffit d'activer le routage dessus.

> 📢  A retenir : La mission du routeur consiste essentiellement __à déterminer sur lequel de ses ports__ il doit réacheminer les paquets reçus : il doit le faire __très vite__ et __s'adapter__ à un environnement qui change (routes qui apparaissent et disparaissent).

## Principe simplifié

Le routage est la base du fonctionnement d'Internet.
Lorsqu’il reçoit un paquet, un routeur l’__analyse__ pour récupérer l’adresse de sa __destination__. En fonction de cette adresse, il doit __choisir vers quel routeur voisin__ retransmettre ce paquet pour le faire progresser vers sa destination.
Il choisit ce voisin à l’aide de sa __table de routage__, qui associe les adresses de destination à des adresses de routeurs. De cette manière, un paquet __transite de routeur en routeur__ jusqu’au client ou au serveur à qui il est destiné.

> 📢  A retenir : L'__objectif du routage IP__ est de trouver le meilleur chemin (le plus court, le plus pertinent, etc...) pour amener chaque paquet à sa __destination__.  

# Table de routage

## Définition

Chaque routeur possède une table de routage. Une table de routage peut être vue comme un tableau donnant pour __chaque destination__ connue par le routeur __la "porte de sortie" à emprunter__ ainsi que l'efficacité de cette route (selon différents critères en fonction des algorithmes utilisés) et contient donc les informations permettant au routeur d’envoyer le paquet de données dans la "bonne direction".

Un routeur possède plusieurs interfaces réseau (eth0, eth1, …), par lequel il est connecté à des sous-réseaux (autre routeur, réseau local, …) au sein desquels il possède une adresse IP.

![](./img/tab_rout.png)  

Dans la table de routage d’un routeur, on trouve les informations suivantes :

* Les adresses IP du routeur
* Les adresses IP des sous-réseaux auquel il est connecté
* Les routes (directions à prendre) qu’il faut suivre pour atteindre un réseau
  * route par défaut (il en faut bien une)
  * routes statiques (configurées explicitement par l’administrateur)
  * routes dynamiques (apprises par des protocoles de routage dynamique)

Chaque ligne de la table contient une route :

* l’adresse du réseau de destination
* la direction à prendre pour l’atteindre :
  * Interface de sortie du routeur (adresse du routeur sur le sous-réseau de sortie)
  * Passerelle (adresse de la prochaine machine sur le sous-réseau de sortie)
* la distance à parcourir (la métrique) avant de l’atteindre

Lorsqu’un routeur reçoit un paquet, il récupère l’adresse du réseau de destination :

* si cette adresse est dans sa table de routage, il envoie le paquet vers l’interface associée,
* dans le cas contraire le paquet est envoyé via l’interface par défaut.

_Exemples_ :

_si le routeur reçoit un paquet à destination de l’ordinateur 192.168.7.2 / 24, sa table de routage pourra contenir la route suivante :_ 

| Réseau destination | Passerelle | Interface | Métrique |
|:------------------:|:----------:|:---------:|:--------:|
| 192.168.7.0/24     |            | eth1      | 1        |

_l’ordinateur est directement relié au routeur,_

* _il n’y a donc pas besoin de passerelle pour l’atteindre_
* _la métrique est de 1 (un seul « saut »)_

_si le routeur reçoit un paquet à destination de l’hôte 172.21.34.21 /16, sa table de routage pourra contenir la route suivante :_

| Réseau destination | Passerelle | Interface | Métrique |
|:------------------:|:----------:|:---------:|:--------:|
| 172.21.0.0/16      | 10.1.2.2   | eth0      | 8        |

_si le routeur reçoit un paquet à destination d’un réseau qui n’est pas dans sa table, il choisit la route par défaut :_  

| Réseau destination | Passerelle | Interface | Métrique |
|:------------------:|:----------:|:---------:|:--------:|
| défaut             | 10.1.2.2   | eth0      | 1        |

📝 _Remarque : en pratique une table de routage ne comporte que des adresses IP. Par conséquent :_

* _l’adresse du réseau de destination n’est pas au format CIDR mais au format IP réseau+masque réseau_
  192.168.7.0 /24 → 192.168.7.0 et 255.255.255.0
* _l’interface est décrite par la propre adresse IP du routeur dans le sous-réseau auquel il est connecté avec cette interface_
  eth1 → 192.168.7.254
* _le réseau de destination de la route par défaut est noté 0.0.0.0_

On peut trouver dans une table de routage plusieurs lignes pour une même destination, il peut en effet, à partir d’un routeur donné, exister plusieurs chemins possibles pour atteindre la destination. Dans le cas où il existe __plusieurs chemins possibles__ pour atteindre la même destination, le routeur va choisir __le « chemin le plus court«__ , celui ayant la valeur de métrique la plus petite (un réseau directement lié à un routeur aura une métrique de 1). 
Pour les réseaux dont la métrique est supérieure à 1, il existe 2 méthodes :  

* le __routage statique__ : chaque ligne doit être renseignée « à la main ». Cette solution est seulement envisageable pour des très petits réseaux ; 
* le __routage dynamique__ : tout se fait « automatiquement », on utilise des protocoles, partagés par tous les routeurs du réseau, qui vont leur permettre d’échanger des informations sur l’état du réseau afin de remplir leur table de routage automatiquement.

# Protocoles de routage

Un réseau de réseaux comportant des routeurs peut être modélisé par un __graphe__ : chaque routeur est un __sommet__ et chaque liaison entre les routeurs ou entre un routeur et un switch est une __arête__. Les algorithmes utilisés par les protocoles de routages sont donc des algorithmes issus de la __théorie de graphes__. (vu plus tard dans l'année).  

## Protocole RIP : Routing Information Protocole

### Vecteur de distance

Initialement (à la mise sous tension), la table de routage d’un routeur contient uniquement des informations sur ses __voisins directs__ (ceux auxquels il est connecté).

![](./img/RIP.png)

_Initialement (mise sous tension) la table de routage de R1 contient uniquement les réseaux 192.168.1.0 /24 et 10.1.1.0 /30._

__Table de routage de R1__

| Réseau destination | Passerelle | Interface | Métrique |
|:------------------:|:----------:|:---------:|:--------:|
| 192.168.1.0/24     |            | wlan0     | 1        |
| 10.1.1.0/30        |            | eth1      | 1        |

_Aucune passerelle n’est spécifiée car le routeur peut atteindre le réseau destination directement._

Chaque routeur envoie périodiquement (__toutes les 30 secondes__), à tous ses voisins (routeurs adjacents), un __message__ contenant :

* la liste de toutes les __adresses de réseaux__ qu’il connait (ses voisins directs et ceux qu’il a reçu auparavant)
* leur __métrique__ (le nombre de sauts pour les atteindre)

> 📢 A retenir : Ce couple d’informations (réseau, métrique) est appelé __vecteur de distance__.  

### Mise à jour

À chaque réception d’un message de ce type, le routeur met à jour sa table de routage avec les informations reçues. Quatre cas peuvent se présenter :

1. il découvre une nouvelle route vers un sous réseau qu’il ne connaissait pas encore : il l’ajoute à sa table
2. il découvre une nouvelle route plus courte vers un sous réseau qu’il connaissait déjà : il remplace l’ancienne route par la nouvelle
3. il reçoit une nouvelle route plus longue vers un sous réseau qu’il connaissait déjà : il ne fait rien
4. il reçoit une route existante dans sa table (passant par le même voisin), mais plus longue. Cela signifie que la route s’est allongée (panne ?) : il met sa table à jour.

Pour renseigner la colonne « métrique », le protocole utilise le nombre de sauts, autrement dit, le nombre de routeurs qui doivent être traversés pour atteindre le réseau cible.  

_Exemple : le routeur R1 reçoit des messages de la part de son seul voisin R3. Ce message contient les vecteurs de distance suivants :_

* _(10.1.2.0 /30 , 1)_
* _(10.1.3.0 /30 , 1)_
* _(10.1.4.0 /30 , 1)_
* _et tous les vecteurs de distance concernant les autres réseaux qu’il « connait »._

_Du point de vue de R1, R3 (d’adresse 10.1.1.2 /30) est une __passerelle__._

Sa table de routage devient alors :  

__Table de routage de R1__  

| Réseau destination | Passerelle       | Interface | Métrique |
|:------------------:|:----------------:|:---------:|:--------:|
| 192.168.1.0/24     |                  | wlan0     | 1        |
| 10.1.1.0/30        |                  | eth1      | 1        |
| __10.1.2.0 /30__   | __10.1.1.2 /30__ | __eth1__  | __2__    |
| __10.1.3.0 /30__   | __10.1.1.2 /30__ | __eth1__  | __2__    |
| __10.1.4.0 /30__   | __10.1.1.2 /30__ | __eth1__  | __2__    |

Le protocole RIP s’appuie sur l’__algorithme de Bellman-Ford__ (algorithme qui permet de calculer les plus courts chemins dans un graphe).

### Délai de convergence

On appelle __délai de convergence__ le temps nécessaire à ce que l’ensemble des routeurs soient configurés pour offrir les meilleurs routes possible. A chaque modification du réseau (ajout ou suppression de routeurs), il faut un certain temps pour que les échanges de messages RIP mènent à une situation stable.

C’est pour limiter ce délai de convergence que le protocole RIP est limité à 15 sauts.

### Détection des pannes

Lorsqu’un routeur ne reçoit pas de réponse de la part d’un autre routeur à une demande RIP (après un certain laps de temps, 3 minutes), il considère que le routeur en question est en panne.

Afin qu’aucun paquet ne soit plus dirigé dans cette direction, il prévient ses voisins en leur envoyant une __métrique égale à 16__ (plus grande valeur possible pour le protocole RIP) concernant toutes les routes passant par le routeur qui ne répond pas.

### Boucle de routage

Une boucle de routage est le phénomène qui se produit lorsqu’un paquet tourne en boucle et ne peut jamais atteindre sa destination.

Différentes règles dans le protocole RIP permettent d’éviter que cela se produise, et notamment la règle _split horizon_, qui interdit à un routeur d’envoyer une information de routage via le routeur qui lui a envoyé.

## Protocole OSPF : Open Shortest Path First

Ce protocole de routage dynamique est basé sur la __bande passante des liaisons__. Ce n’est plus seulement le nombre de routeurs franchis qui importe mais le débit binaire possible entre les routeurs. Ce débit dépend du matériel, de leur disponibilité, du support de communication (fibre optique, liaison hertzienne, etc.).

### Calcul de la métrique

$` métrique = \frac{débit\ de\ référence}{débit\ du\ lien}`$  
avec une valeur pour le débit de référence égale à 100Mb/s

📝 _Remarque_ : la plus petite valeur pour cette métrique a été fixée à 1. Pour tout débit supérieur à 100Mb/s, par exemple une liaison à 1Gb/s, la métrique aura la valeur 1
Exemple : pour une liaison à 10Mb/s, la métrique sera de 10

### Fonctionnement

Le fonctionnement du protocole OSPF est découpé en deux grandes étapes :

* chaque routeur, après avoir été initialisé, tente de __découvrir ses voisins__ afin d'établir une relation de voisinage : les machines dans ce protocole sont classées en différentes zones. Les routeurs limitent leur recherche de voisins dans la zone qui leur est affectée :
  
  * le routeur choisit un __identificateur unique__, par exemple sa plus grande adresse IP parmi celles de ses sous-réseaux ;
  
  * le routeur poursuit en __envoyant des messages__ de type HELLO à travers tous ses interfaces réseaux ; 
  
  * quand un autre routeur reçoit un paquet HELLO du routeur, il vérifie si son identificateur apparaît déjà dans sa liste de voisins :
    
    * Si c'est le cas, il envoie un accusé de réception
    * Sinon il répond en envoyant __les informations dont il dispose sur la topologie du réseau__. 
      Les routeurs d'une même zone ont ainsi toute la même vision du réseau.

* l'algorithme de type __algorithme de Disjktra__ pour calculer les __meilleures routes__(coût le plus faible) entre chaque routeur de la zone est ensuite exécuté.  Les tables de routage sont ainsi mises à jour.  

Le protocole OSPF est donc bien plus performant que RIP mais plus complexe d'utilisation et destiné aux grands réseaux.
Les avantages sont par exemple : 

* pas de limite de sauts
* permet à chaque routeur une connaissance complète des réseaux au sein d'une zone
* élimine le danger des boucles de routage
* les mises à jour ne sont envoyées que lors d'un changement de topologie

> 📢 A retenir :  
> -RIP (Routing Information Protocol) : le plus court chemin est déterminé par le __nombre de sauts__ ; la mise à jour s'effectue toutes les 30 s ; limitée à 15 sauts ; convient pour les réseaux de petite taille.  
> -OSPF (Open Short Path First) : le plus court chemin est déterminé par __le coût des routes__ ; pas de limite de sauts ; la mise à jour s'effectue seulement en cas de changement ; adapté aux grands réseaux.

Dans l'exemple ci-dessous on voit ainsi :

* RIP : R1--> R2 --> R5  
* OSPF : R1 --> R3 --> R4 --> R5

![](./img/comp_rip_ospf.png)

Sources :

* cours NSI L Petit  
* Cours NSI C Faury Lycée Blaise Pascal à Clermond Ferrand  
* NSI Terminale Ellipses T. Balabonski,S. Conchon, JC. Filliatre, K Nguyen  
* NSI Terminale Nathan les vrais exos S Pasquet M Leopoldoff  
