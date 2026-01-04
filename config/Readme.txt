J'ai ajouté ces 3 linges en fin du mon mosquitto.conf :
listener 1883 0.0.0.0  (Écoute sur le port 1883, toutes les interfaces réseau)
allow_anonymous false  (Refuse les connexions sans authentification)
password_file C:\Users\ihebz\Desktop\mosquitto\passwd  (Utilise le fichier de mots de passe)

le fichier de mots de passe :
mosquitto_passwd -c C:\Users\ihebz\Desktop\mosquitto\passwd iheb
Ensuite, j'ai entré le mot de passe: zapatista00