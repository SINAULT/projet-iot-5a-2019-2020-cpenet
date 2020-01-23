# Configuration Passerelle - Cloud

## Envoi des données
Ce code est utilisé pour envoyer les données recues sur le Raspberry Pi vers Ubidots.<br/>
Il crée une requête HTTP avec les données à envoyer.
<br/>
<br/>

Pour plus de simplicité, et pour ne pas avoir à toucher au code, il faut passer ,dans l'ordre, et en argument de ce code les 5 variables récupérees (temperature,pression,altitude,humidité,feu).
Lorsque que vous créez votre espace Ubidots, il est necessaire de changer le TOKEN, présent en haut du code, par celui propre à votre compte.
<br/>
Afin d'assurer une tracabilité, les donneés envoyées sont sauvegardées dans un fichier de logs : 'logs.txt', grâce à la fonction  write_log.
<br/>
<br/>
Ce script est ensuite appellé par le script read_send.py, qui recupere les données de l'arduino et appelle ce programme ci en passant en argument les données.

## Configuration cloud
La première étape consiste en la création d'un compte sur ubidots, ensuite dans la partie devices, on effectue le lien entre Ubidots et notre device que l'on nomme comme on le veut, ce nom est important car il devra être le même que celui indiqué dans le code d'envoie des donées.\
Ensuite la seconde étape consiste en la création des différentes variables que nous allons utilisées : on clique alors sur le "+" pour ajouter une nouvelle variable dont le nom doit aussi être le même que celui indiqué dans le code d'envoi\
Afin d'avoir une actualisation des donées recues via les capteurs, on doit aller chercher le token dans l'onglet user, ce token est alors à copier dans la partie "TOKEN =" du code d'envoi\
L'étape suivante consiste à créer un dashboard regroupant les divers widgets et graphiques qui permettent d'analyser et manager les datas\
on associe un widget et un suivi graphique à chaque variables\
Enfin, dans la section datas, on peut créer des events, comme des alertes en fonction de l'évolution des parametres qui permettent l'envoie de mail ou même de rapport quotidien des suivis des différentes variables.

