# Configuration BeagleBone Black (BBB)

![alt Beaglebone](../images/bbb.jpg)

## 

## Lecture des données de l'Arduino

### Utilisation

Lancer le script read_send.py avec python3 sur le Raspberry. <br/>
ATTENTION : le port de lecture 
est défini dans le script, il nécessite probablement d'être changé. On peut consulter la liste 
des ports ouverts avec ```ls /dev/tty*``` <br/>
ATTENTION : si le script tourne déjà, le lancer une 
seconde fois depuis un autre terminal fera planter les deux.

### Fonctionnement

Le script read_send.py permet de lire les données envoyées depuis le port série 1 de 
l'Arduino. Lorsque le script s'exécute, les données au format JSON sont lues en permanence 
jusqu'à ce que le symbole '}' apparaisse, méthode read_until() de la classe Serial. <br/>

Lorsque que ce symbole apparaît, on a alors reçu une trame de la forme
``` { Clé: valeur, Temperature : 26.25, Altitude : 12.0 ... } ```
que l'on convertit du type bytes vers une chaîne de caractères, méthode decode(). <br/>

On parse ensuite la chaîne JSON, méthode json.loads(), pour récupérer les valeurs associées 
aux clés et les utiliser ensuite. <br/>

On appelle ensuite le script send_data.py en passant les valeurs récupérées en argument.
 -> voir ../cloud-code/ pour la documentation du script d'envoi de données. <br/>
