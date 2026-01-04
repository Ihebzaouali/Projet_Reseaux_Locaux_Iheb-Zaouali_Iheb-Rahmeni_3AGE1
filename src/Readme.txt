----- Ouvrir Mosquitto : 
Terminal 1 : (cmd en tant qu'administrateur) 
cd \Users\ihebz\Desktop\mosquitto > mosquitto -c mosquitto.conf -v 


Ouvrir le fichier "stm32_mqtt_sensors.ino" puis exécuter le code 


------Tests :
1)
Terminal : (cmd en tant qu'administrateur) 
cd \Users\ihebz\Desktop\mosquitto> netstat -an | findstr :1883  
ipconfig 
ping 192.168.0.135 ( Adresse IP WIFI PC - Broker local )
ping 192.168.0.22 ( Adresse IP du carte ) 

2)
Terminal 1: (cmd en tant qu'administrateur) 
cd \Users\ihebz\Desktop\mosquitto> mosquitto_sub -h 192.168.0.135 -t "/ihebz" -u iheb -P zapatista00 

Terminal 2: (cmd en tant qu'administrateur)
cd \Users\ihebz\Desktop\mosquitto> mosquitto_pub -h 192.168.0.135 -t "/ihebz" -m "mynameisiheb" -u iheb -P zapatista00 

----> Résulat affiché sur Terminal 2



----- Affichage du valeurs des topics : s
Terminal : (cmd en tant qu'administrateur)
cd \Users\ihebz\Desktop\mosquitto> mosquitto_sub -h 192.168.0.135 -t "#" -v -u iheb -P zapatista00 (afficher tous les topics)

ou utilisez : 

mosquitto_sub -h 192.168.0.135 -t "/temperature" -t "/Humidite" -t "/Pression" -t "/Accelero_X" -t "/Accelero_Y" -t "/Accelero_Z" -t "/Gyro_X" -t "/Gyro_Y" -t "/Gyro_Z" -t "/Magneto_X" -t "/Magneto_Y" -t "/Magneto_Z" -u iheb -P zapatista00  (Si Broker locale : 192.168.0.135 (adresse ip WIFI))

mosquitto_sub -h "broker.hivemq.com" -t "/temperature" -t "/Humidite" -t "/Pression" -t "/Accelero_X" -t "/Accelero_Y" -t "/Accelero_Z" -t "/Gyro_X" -t "/Gyro_Y" -t "/Gyro_Z" -t "/Magneto_X" -t "/Magneto_Y" -t "/Magneto_Z"  (Si Broker Public : broker.hivemq.com/test.mosquitto.org) 



---- Ouvrir Node-Red : 
Terminal : (cmd en tant qu'administrateur)
cd \Users\ihebz\Desktop\mosquitto> node-red
copier l'adresse du serveur "http://127.0.0.1:1880/" dans le web pour l'affichage et "http://127.0.0.1:1880/ui" pour dashboard






