# Configuration Arduino ou autre
Configurai=tion d'un Arduino MEGA 2560

# Pre reguis 
1. Se rendre sur le site https://www.arduino.cc/, creer un compte et telecharger le plug-in ArduinoCreateAgent-1.1 pour detecter le port Serial.
Ouvrir le Adruino Web Editor et detecter le port serial.
Testet le programme Blink présent dans les exemples sur l'arduino pour verifier le fonctionnement 



2. Ajout des librairies pour les differents capteurs
Les librairies qu'on a utilisé sont mis a disposition sur le git dans le repertoire librairies.
Pour ajouter des librairies, veuillez suivre ces instrutions :


# les capteurs:

Pour ce projet nous avons a disposition 2 clicks:
- Flame CLick 
- Weather Click

Flame Clik est un detecteur de flamme qui fonctionne avec un capteur infrarouge,puisque il y a de l'infrarouge dans la lumiere artificielle et celle du soleil on a etalonné le capteur pour qu'il ne detecte qu'une flamme, en ajustant le potentiometre qui est sur le click.

Concernant le weather click, c'est un capteur 4 en 1, il permet de relever la temperature, la pression, l'humidité et l'altitude.

L'Arduino recupere les données depuis les capteurs et transmet un paquet Json sur le port Serial ( voir gateway_code) 
Exemple formatage Json :
{
  "Temperature": "XXX",
  "Pression": "XXX",
  "Humidité: "XXX",
  "Altitude" : "XXX",
  
}

# Executer porgramme

Il n y a qu'un seul fichier qui pourrait etre executer : Sensors.ino disponible dans le repertoire object_code






