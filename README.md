# Projet IoT
## Équipe

Dylan Synault (Chef de projet)<br />
Nicolas BOSIA<br />
Jérémy ROQUIN<br />
Saad KAHOUI<br />
Mehdi LARIBI<br />

## Description du Projet

Le projet de l'équipe CPE-NET est la création d'un système IOT pour la detection et l'anticipation des incendies. Ce projet utilise plusieurs capteurs 'click' ainsi qu'un Arduino Mega et un RaspberryPi.<br />
<br />
Notre idée originale était d'utiliser une communication GSM entre l'arduino et le Raspberry, en y implémentant OpenBTS.<br />
Par manque de temps et à cause de problèmes techniques, nous n'avons pas reussi à faire fonctionner cette liaison.<br />
Ainsi, et afin d'avoir une chaine de transmission complète, nous avons pour l'instant connecté le Raspberry et l'arduino par une liaison série.<br />
<br />
Voici ci-dessous un schéma de fonctionnement du projet. <br />
<br />

![alt text](https://github.com/CPELyon/projet-iot-5a-2019-2020-cpenet/blob/master/images/schema.png)

### Capteurs

Nous utilisons un capteur 'météo' qui relève des données d'humidité, de température, de pression et d'altitude, ainsi qu'un detecteur de flamme.<br />

### Cas d'utilisation

L'idée serait de placer l'arduino équipé des capteurs dans une forêt (sur un arbre par exemple) et alimenté d'une batterie.
Ainsi, le système enverrait des données au raspberry,qui est connecté à internet, et qui transmets les données à la plateforme qui les récolte : Ubidots.
Ce système a pour vocation de détecter les incendies et les conditions favorables à un départ d'incendie afin d'agir de facon proactive.
Si le système détecte une température trop elevée ainsi qu'une humidité très faible, il est capable de prévenir, via l'interface ou un mail d'alerte, qu'il y a potentiellement des risques d'incendie dans la zone du capteur.

## Répartition des tâches

| Dylan SINAULT | Nicolas BOSIA   | Saad Kahoui   | Jérémy ROQUIN |  Mehdi LARIBI | 
| :------------ | :-------------  | ------------- | ------------- | ------------- |
| Configuration passerelle IOT | Liaison entre la passerelle IOT et le service Cloud | Paramétrage des capteurs de flamme et de météo | Liaison entre les Objets Communicant et la passerelle IOT | Configuration du service Cloud et Interface Web |


### Suivi journalier

__10 janvier :__

Notre groupe travaille sur les capteurs Weather Click et Flame Click.

Création Team sur Github, association d’une première interface web hébergée sur Github Pages ( https://cpelyon.github.io/projet-iot-5a-2019-2020-cpenet/ )
Création compte d’essai Microsoft Azure et démarrage d’un App Service pour explorer l’hébergement cloud.
Récupération des Datasheets des différents composants / capteurs.

Elaboration du schéma fonctionnel.
Réflexion sur différents scénarii possibles pour l’utilisation de nos capteurs.

__20 Janvier :__

Dylan : Installation d’OpenBTS et ses dépendances + driver USRP

Mehdi : prise en main d’azure et installation des logiciels elasticsearch qui va nous permettre de creer une base de donées ainsi que de kibana et beats qui permettent de gérer les données et de les traiter dans le cloud
travail à finir : accéder aux interfaces graphiques de kibana et elasticsearch à l’aide d’une redirection des ports 

Nicolas : Recolte des données via arduino. Le module est fonctionnel. A voir le traitement pour décider a partir de quand on déclenche alarme.

Jérémy : Compréhension module GSM, chinage de code Arduino pour le 
module SIM800H, importation de librairies avec code semblant utilisable

Saad : Prise en main des différents capteurs, installation des outils nécessaire et debug des problèmes sur Arduino. Mise en place du code pour lire et afficher les différentes informations depuis le capteur Weather et aussi depuis le capteur flame click.

__21 Janvier :__

Dylan : Installation et configuration d’OpenBTS et ses dépendances à travers l’environnement Docker.
Reprise d’un Dockerfile adapté pour une architecture AMD64 et création d’un nouveau Dockerfile correspondant à l’architecture ARM7 du Raspberry Pi.

Mehdi : abandon de azur et d’elastic search, passage sur ubidots et acquisition via un script python de données de test, acquisition OK et transmission des données de raspberry vers ubidots OK, création des premiers dashboards avec graphique et analyse des données recues  
travail à finir : finir les dashboards, mettre en place la transmission des mails d’alerte et des seuils d’alerte pour les différentes variables 

Nicolas : installation DBAzure et envoie des données via methode post dans la DB. Configuration ubidots avec mehdi, ecriture du script d’envoi des données à la réception d’un sms en passant en argument les parametres.
Reste a cleaner et commenter le script puis interconnecter avec reception des sms.

Jérémy : Essai de différentes librairies GSM, débuggage. Essais avec différentes cartes pins. Cablâge physique sur board pour débugguer. Le module GSM pose toujours de nombreux problèmes de compréhension.

Saad : Installation des librairies Json, formatage et codage des données récupérer auprès des capteurs en paquet JSON, déboggage des problèmes GSM et GPRS. Reste à récupérer les paquets JSON et les transmettre sur l’antenne GSM. 

__22 Janvier :__

Dylan : Installation et configuration d’OpenBTS et ses dépendances à travers l’environnement Docker.
Reprise d’un Dockerfile adapté pour une architecture AMD64 et création d’un nouveau Dockerfile correspondant à l’architecture ARM7 du Raspberry Pi.

Mehdi : réalisation du dashboard comprenant les widgets suivant : suivi en temps réelles de toutes les données : température, altitude, pression et humidité, mise en place du service d’alertes via mail et appel vocal en définissant un seuil d’alerte sur chaque donnée et en combinant divers données telle que temperature superieure à 40° depuis plus de 2 min et humidité en dessous de 2% depuis plus de 2 min etc 
travail à finir : attendre la transmission via la chaîne de commande afin de vérifier que le dashboard et les alertes s‘actualisent bien, le test est OK avec un script local  

Nicolas : Remaniement du code python d’envoi des donnees a ubidot. Code commenté. Tracabilité des envois dans un fichier de log. Reste à régler le format de ce fichier.
Experimentation de communication radio ( avec l’adaptateur USB/VGA)
Premieres recherches autour de 6LoWPAN.

Jérémy : Poursuite de débuggage GSM. Découverte de certains éléments bloquants auparavant, mais toujours impossible de recevoir une réponse aux commandes AT envoyées en serial sur le click.
Experimentation de communication radio ( avec l’adaptateur USB/VGA)
Premieres recherches autour de 6LoWPAN.

Saad : Premieres recherches autour de 6LoWPAN.

## Procédure de mise en place de votre chaîne IoT

## Conclusions et recommandations
