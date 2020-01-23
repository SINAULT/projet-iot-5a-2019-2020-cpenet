 # Pistes explorées 
 
 Les fichiers de ce dossier regroupent les différentes pistes explorées par les membres du groupe
 
 ## OpenBTS pour Raspberry 3
 
 Initialement OpenBTS devait servir à la liaison GSM entre la passerelle IOT et le capteur GSM. 
 Le but était donc de créer une image Docker spécialement conçue pour l'utilisation du logiciel OpenBTS pour une architecture ARM64.
 
 J'ai fait des recherches sur des images existantes dont celle-ci sur ce repo Docker Hub : https://hub.docker.com/r/m1mbert/openbts-xenial
 
 Cette image peut être utilisée sur des architectures AMD64 et non ARM64. De ce fait, l'objectif était de modifier le Dockerfile afin de le rendre utilisable pour notre type d'architecture.
 
 __La démarche :__
 
En m'inspirant des lignes du Dockerfile, je suis parti d'une image Docker Ubuntu:xenial vierge et j'ai tenté d'installer ligne par ligne les différentes couches.

Après plusieurs jours de tentatives de construction de l'image, je suis arrivé à un blocage : La compilation du code d'OpenBTS en .deb pour la bonne architecture. Il semblerait que les différentes versions de "gcc" et "g++" ne permettent pas de compiler le code d'OpenBTS mais que tout le reste fonctionne.

__Le résultat :__

A la fin de mes recherches, j'ai pu avoir une image Docker qui fonctionne pour l'architecture du Raspberry 3 avec toutes les dépendances qui sont demandées par OpenBTS ainsi que tous les services opérationnels. Cependant du fait de l'absence du module OpenBTS-CLI il n'est pas possible d'utiliser les commandes CLI d'OpenBTS.

__Installation :__

__Prérequis :__

- Avoir un OS Ubuntu 16.04 ARM64 minimum.
- Avoir Docker d'installé sur son Raspberry Pi 3.
- Accès Internet.

$ git clone https://github.com/CPELyon/projet-iot-5a-2019-2020-cpenet/tree/master/pistes-explorees/openbts-docker.git

$ cd /openbts-docker

__POUR CONSTRUIRE L'IMAGE DOCKER :__

$ docker build --network=host --add-host=<user-de-la-machine-hôte>:127.0.1.1 -t openbts-xenial .

__POUR DEMARRER LE CONTENEUR :__

$ docker run -dti --privileged --net=host --name=openbts openbts-xenial:latest

__POUR DEMARRER UN TERMINAL DANS LE CONTAINER :__

$ docker exec -it openbts /bin/bash

__UNE FOIS ENTRE, VOUS POUVEZ LANCER LE SERVICE OPENBTS :__

$ /home/cxlbadm/openbts_systemd_scripts/openbts-start.sh

__VOUS SEREZ A PRESENT DANS OPENBTS :__

$ /OpenBTS/

Si tout aurait bien fonctionné nous aurions du avoir la possibilité d'utiliser les commandes CLI d'OpenBTS. ($ /OpenBTS/OpenBTSCLI).

Si vous souhaitez poursuivre il faudra trouver un moyen de compiler la partie OpenBTS en architecture ARM64 et ajouter une couche dans le Dockerfile copiant le fichier .deb .
