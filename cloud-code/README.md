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

Pour lancer un code en python, on utilise la commande python3 $nom_du_script
<br/>

On lance donc ici :
```

python3 read_send.py

```
## Configuration cloud

La première étape consiste à créer d'un compte sur [Ubidots](https://ubidots.com/) : 
<br/> 
<br/> 
Une fois votre compte créé, on effectue, dans le sous menu **Devices**, le lien entre Ubidots et le device qui doit envoyer les données. Il est important de mettre le même nom dans le code d'envoi et dans l'interface.

<br/>

Il faut ensuite créer les différentes variables : à l'aide du "+", en haut à droite.
<br/> 
De la même manière, le nom de la variable doit être identique à celui dans le code d'envoi.
<br/> 
<br/> 
Afin d'avoir une actualisation des donées recues via les capteurs, on doit aller chercher le token dans l'onglet user, ce token est alors à copier dans la partie "TOKEN =" du code d'envoi.

L'étape suivante consiste à créer un dashboard regroupant les divers widgets et graphiques qui permettent d'analyser et manager les datas
<br/> 
<br/> 
On associe ensuite un widget et un suivi graphique à chaque variables
<br/> 
Enfin, dans la section **Datas**, on peut créer des évènements et des alertes en fonction de l'évolution des paramètres : ceux ci vont permettre l'envoi de mail ou même de rapport quotidien de suivis des différentes variables.
<br/> 
Vous pouvez ainsi personnaliser la configuration du Ubidots pour que celle-ci corresponde parfaitement à votre usage.
 
<br/> 
<br/> 

![alt text](https://github.com/CPELyon/projet-iot-5a-2019-2020-cpenet/blob/master/images/ubidots.png)
