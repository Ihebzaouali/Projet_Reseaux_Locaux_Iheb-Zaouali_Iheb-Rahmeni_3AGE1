# Projet IoT : Système de Monitoring Multi-Capteurs avec STM32, MQTT, Node-RED et MongoDB

<div align="center">

![STM32](https://img.shields.io/badge/STM32-L475E--IOT01A-blue?style=for-the-badge&logo=stmicroelectronics)
![MQTT](https://img.shields.io/badge/MQTT-Protocol-purple?style=for-the-badge&logo=mqtt)
![Node-RED](https://img.shields.io/badge/Node--RED-Workflow-red?style=for-the-badge&logo=nodered)
![MongoDB](https://img.shields.io/badge/MongoDB-Database-green?style=for-the-badge&logo=mongodb)

**Projet de Réseaux Locaux - ENIT 2026**

 [📹 Vidéo Démo](#-démonstration) •[📖 Documentation](#-table-des-matières) • [🚀 Installation](#-installation-rapide)

</div>

---

## 👥 Auteurs

**Iheb Zaouali** & **Iheb Rahmeni**

**Encadrant** : Dr. Khaled Jelassi  
**Établissement** : ENIT - École Nationale d'Ingénieurs de Tunis  
**Cours** : Réseaux Locaux (3AGE1)

---

## 📋 Table des Matières

- [🎯 Aperçu du Projet](#-aperçu-du-projet)
- [✨ Fonctionnalités](#-fonctionnalités)
- [🏗️ Architecture](#️-architecture)
- [🔧 Composants](#-composants)
- [📊 Métriques](#-métriques)
- [🚀 Installation Rapide](#-installation-rapide)
- [📱 Dashboard](#-dashboard)
- [🗄️ Base de Données](#️-base-de-données)
- [⚠️ Problèmes et Solutions](#️-problèmes-et-solutions)
- [🎥 Démonstration](#-démonstration)
- [🎓 Conclusion](#-conclusion)
- [🚀 Perspectives](#-perspectives)

---

## 🎯 Aperçu du Projet

Système IoT complet de **monitoring environnemental et de détection de mouvement** en temps réel, utilisant :
- 📡 **STM32L475E-IOT01A** pour l'acquisition de données
- 🔌 **MQTT** pour la communication
- 🔄 **Node-RED** pour l'orchestration
- 🗄️ **MongoDB** pour le stockage
- 📊 **Dashboard Web** pour la visualisation

### 🎯 Cas d'Usage

- 🌡️ Surveillance environnementale (température, humidité, pression)
- 🏃 Détection de mouvement et d'orientation
- 📈 Analyse historique des données
- 🚨 Système d'alerte intelligent
- 📊 Station météo connectée

---

## ✨ Fonctionnalités

### Capteurs Embarqués (12 valeurs)

| Catégorie | Capteurs | Valeurs |
|-----------|----------|---------|
| **Environnement** | HTS221, LPS22HB | Température, Humidité, Pression |
| **Mouvement** | LSM6DSL | Accéléromètre X/Y/Z, Gyroscope X/Y/Z |
| **Magnétique** | LIS3MDL | Magnétomètre X/Y/Z |

### Fonctionnalités Clés

- ✅ **Acquisition temps réel** : 1 Hz (1 lecture/seconde)
- ✅ **Communication WiFi** : 802.11 b/g/n
- ✅ **Publication MQTT** : 12 topics différents
- ✅ **Reconnexion automatique** : En cas de perte de connexion
- ✅ **Dashboard interactif** : 3 pages de visualisation
- ✅ **Stockage historique** : Base MongoDB
- ✅ **Graphiques temps réel** : Mise à jour < 1 seconde

---

## 🏗️ Architecture

### Architecture Globale

```
┌─────────────────────┐
│  STM32L475E-IOT01A  │
│   ┌─────────────┐   │
│   │  6 Capteurs │   │
│   │  (12 axes)  │   │
│   └──────┬──────┘   │
│          │          │
│   ┌──────▼──────┐   │
│   │ WiFi Module │   │
│   └──────┬──────┘   │
└──────────┼──────────┘
           │ MQTT
           ▼
   ┌───────────────┐
   │    Mosquitto  │
   │  MQTT Broker  │
   └───────┬───────┘
           │
           ▼
   ┌───────────────┐
   │   NODE-RED    │
   │   Workflow    │
   └───┬───────┬───┘
       │       │
   ┌───▼───┐ ┌─▼──────┐
   │MongoDB│ │Dashboard│
   └───────┘ └────────┘
```

### Topics MQTT (12 topics)

| # | Topic | Type | Unité |
|---|-------|------|-------|
| 1 | `/temperature` | Float | °C |
| 2 | `/Humidite` | Float | % |
| 3 | `/Pression` | Float | hPa |
| 4-6 | `/Accelero_X/Y/Z` | Integer | mg |
| 7-9 | `/Gyro_X/Y/Z` | Float | dps |
| 10-12 | `/Magneto_X/Y/Z` | Integer | mGauss |

---

## 🔧 Composants

### Matériel

- **Microcontrôleur** : STM32L475E-IOT01A (ARM Cortex-M4)
- **Module WiFi** : Inventek ISM43362-M3G-L44
- **Capteurs** : HTS221, LPS22HB, LSM6DSL, LIS3MDL

### Logiciel

- **Langage** : C/C++ (Arduino), JavaScript (Node-RED)
- **IDE** : Arduino IDE 2.x
- **Broker MQTT** : Mosquitto 2.x (Windows local
- **Orchestration** : Node-RED 3.x
- **Base de données** : MongoDB Atlas (Cloud NoSQL)
- **Dashboard** : Node-RED Dashboard
- **Protocoles** : MQTT, WiFi 802.11, SPI, I2C, UART

### Bibliothèques Arduino

```cpp
#include <stm32l475e_iot01.h>
#include <stm32l475e_iot01_accelero.h>
#include <stm32l475e_iot01_gyro.h>
#include <stm32l475e_iot01_hsensor.h>
#include <stm32l475e_iot01_magneto.h>
#include <stm32l475e_iot01_psensor.h>
#include <stm32l475e_iot01_tsensor.h>
#include <WiFiST.h>
#include <MQTTClient.h>
```

---

## 📊 Métriques

### Code Source

| Composant | SLOC | Langage |
|-----------|------|---------|
| **Arduino STM32** | ~280 lignes | C/C++ |
| **Node-RED Functions** | ~120 lignes | JavaScript |
| **Total** | ~400 lignes | - |

### Performances Mesurées

| Métrique | Valeur | Objectif | Status |
|----------|--------|----------|--------|
| Fréquence acquisition | 1 Hz | 1 Hz | ✅ |
| Latence MQTT | < 50ms | < 100ms | ✅ |
| Perte de paquets | < 0.1% | < 1% | ✅ |
| Temps reconnexion | 5-10s | < 15s | ✅ |
| CPU Node-RED | < 5% | < 20% | ✅ |
| Uptime | > 24h | > 12h | ✅ |

### Ressources

- **SRAM STM32** : ~15-20 KB / 128 KB (15%)
- **Flash STM32** : ~100-150 KB / 1024 KB (12%)
- **RAM Node-RED** : ~150 MB
- **Croissance MongoDB** : ~1 MB/jour

---

## 🚀 Installation Rapide

### Prérequis Windows

Vérifier que vous avez installé :
- **Node.js** : v18.x ou supérieur → [Télécharger](https://nodejs.org/)
- **Arduino IDE** : v2.x (ou v1.8.6+) → [Télécharger](https://www.arduino.cc/en/software)
- **Git** (optionnel) → [Télécharger](https://git-scm.com/)

Vérifier les versions dans PowerShell ou CMD :
```powershell
node --version    # Doit afficher v18.x.x ou supérieur
npm --version     # Doit afficher 9.x.x ou supérieur
```

**Note importante** : Ce projet utilise MongoDB Atlas (cloud) au lieu d'une installation locale, et Mosquitto MQTT Broker local sur Windows.

---

### 1️⃣ Installation Mosquitto MQTT Broker (Windows)

#### Prérequis - Dépendances Windows

Pour Windows 7/8/10, installer d'abord les dépendances :

**1. OpenSSL** (obligatoire)
- Télécharger depuis : https://slproweb.com/products/Win32OpenSSL.html
- Installer `Win32 OpenSSL v1.1.1` ou version supérieure
- Les DLLs nécessaires : `libeay32.dll`, `ssleay32.dll`

**2. pthreads** (obligatoire pour Windows 7/8)
- Télécharger depuis : ftp://sources.redhat.com/pub/pthreads-win32/dll-latest/dll/x86/
- DLL nécessaire : `pthreadVC2.dll`
- Copier dans `C:\Program Files\mosquitto\` ou `C:\Windows\System32\`

#### Télécharger et Installer Mosquitto

1. **Télécharger** la version Windows depuis : https://mosquitto.org/download/
   - Fichier recommandé : `mosquitto-1.6.x-install-windows-x64.exe` ou version plus récente
   - Pour référence : http://www.eclipse.org/downloads/download.php?file=/mosquitto/binary/win32/mosquitto-1.4.8-install-win32.exe

2. **Exécuter l'installeur** en tant qu'administrateur
3. **Installer** dans `C:\Program Files\mosquitto\` (par défaut)
4. **Copier les DLLs** d'OpenSSL et pthreads dans le dossier d'installation

#### Configuration

Créer/modifier le fichier `C:\Program Files\mosquitto\mosquitto.conf` :

```conf
# mosquitto.conf - Configuration de base
listener 1883
allow_anonymous true
log_dest file C:\Program Files\mosquitto\mosquitto.log
log_type all
```

#### Vérifier le Service Mosquitto

**Vérifier si le service est installé** :
```powershell
# Ouvrir services.msc
Win + R → taper: services.msc → Entrée
```

Chercher "Mosquitto Broker" dans la liste des services.

#### Démarrer Mosquitto

**Option 1 : Service Windows (recommandé)**
```powershell
# PowerShell en tant qu'administrateur
net start mosquitto
```

**Option 2 : Ligne de commande manuelle**
```powershell
# PowerShell en tant qu'administrateur
cd "C:\Program Files\mosquitto"
mosquitto.exe -c mosquitto.conf -v
```

**Vérifier que Mosquitto écoute sur le port 1883** :
```powershell
netstat -an | findstr 1883
# Doit afficher: TCP 0.0.0.0:1883 ... LISTENING
```

#### Tester la connexion MQTT

**Test 1 : Subscribe/Publish local**

Dans deux terminaux PowerShell différents :

**Terminal 1 (Subscriber)** :
```powershell
cd "C:\Program Files\mosquitto"
mosquitto_sub.exe -h localhost -t "test" -v
```

**Terminal 2 (Publisher)** :
```powershell
cd "C:\Program Files\mosquitto"
mosquitto_pub.exe -h localhost -t "test" -m "Hello MQTT"
```

Vous devriez voir apparaître "Hello MQTT" dans le Terminal 1.

**Test 2 : Écouter tous les topics**
```powershell
cd "C:\Program Files\mosquitto"
mosquitto_sub.exe -h localhost -t "#" -v
```

Cette commande affichera tous les messages MQTT publiés sur le broker.

---

### 2️⃣ Installation Node-RED (Windows)

#### Installation globale via npm

```powershell
npm install -g --unsafe-perm node-red
```

#### Installer les dépendances Node-RED

```powershell
# Naviguer vers le dossier .node-red
cd %USERPROFILE%\.node-red

# Installer les palettes nécessaires
npm install node-red-dashboard
npm install node-red-node-mongodb

# OPTIONNEL : Pour Firebase (si vous souhaitez aussi tester Firebase)
npm install node-red-contrib-firebase
```

#### Démarrer Node-RED

```powershell
node-red
```

Vous devriez voir :
```
Welcome to Node-RED
===================
[info] Node-RED version: v3.x.x
[info] Node.js  version: v18.x.x
[info] Server now running at http://127.0.0.1:1880/
```

Accès :
- **Node-RED Editor** : http://localhost:1880
- **Dashboard** : http://localhost:1880/ui

#### Importer les Flows du projet

1. Ouvrir http://localhost:1880
2. Menu ☰ (coin supérieur droit) → Import
3. Sélectionner l'onglet "Clipboard"
4. Coller le contenu de votre fichier `node-red/flows.json`
5. Cliquer sur "Import"
6. Positionner les flows sur l'éditeur
7. Cliquer sur **"Deploy"** (bouton rouge en haut à droite)

#### Vérifier l'installation des palettes

Dans Node-RED :
1. Menu ☰ → Manage palette
2. Onglet "Install"
3. Vérifier que `node-red-dashboard` et `node-red-node-mongodb` sont installés

Si non installés, les rechercher et cliquer sur "Install".

---

### 3️⃣ Configuration MongoDB Atlas (Cloud)

#### Créer un compte MongoDB Atlas

1. Aller sur https://www.mongodb.com/cloud/atlas/register
2. Créer un compte gratuit (Free Tier - M0)
3. Créer un nouveau cluster (sélectionner la région la plus proche)

#### Configuration du cluster

**Étape 1 : Créer un utilisateur de base de données**
- Database Access → Add New Database User
- Username: `iot_user` (ou autre)
- Password: `votre_mot_de_passe_sécurisé`
- Database User Privileges: `Read and write to any database`
- Add User

**Étape 2 : Autoriser l'accès réseau**
- Network Access → Add IP Address
- Option 1 (développement) : `0.0.0.0/0` (autoriser tous les IP)
- Option 2 (production) : Ajouter votre IP publique uniquement
- Confirm

**Étape 3 : Obtenir la chaîne de connexion**
- Clusters → Connect → Connect your application
- Driver: Node.js, Version: 4.1 or later
- Copier la connection string :
```
mongodb+srv://iot_user:<password>@cluster0.xxxxx.mongodb.net/?retryWrites=true&w=majority
```

**Étape 4 : Créer la base de données**
- Collections → Create Database
- Database name: `iot_sensors`
- Collection name: `sensor_data`
- Create

#### Configuration dans Node-RED

1. Double-cliquer sur un nœud **mongodb out**
2. Cliquer sur le crayon ✏️ à côté de "Server"
3. Remplir :
   - **Name** : MongoDB Atlas
   - **Host** : `cluster0.xxxxx.mongodb.net` (depuis votre connection string)
   - **Port** : `27017`
   - **Database** : `iot_sensors`
   - **Topology** : ☑️ Use a replica set
   - **Replica set name** : Vide
   - **Use TLS** : ☑️ Coché
4. Onglet **Security** :
   - **Username** : `iot_user`
   - **Password** : `votre_mot_de_passe`
5. Update → Done

#### Vérifier la connexion

Dans Node-RED, déployez et vérifiez les logs. En cas d'erreur, vérifier :
- Username/password corrects
- IP autorisée dans Network Access
- TLS activé
- Connection string correcte

---

### Configuration Arduino

1. **Ouvrir** `src/stm32_mqtt_sensors.ino` dans Arduino IDE

2. **Modifier les credentials WiFi** :
```cpp
char ssid[] = "VOTRE_SSID";
char pass[] = "VOTRE_MOT_DE_PASSE";
```

3. **Modifier l'adresse du broker MQTT** :
```cpp
client.begin("VOTRE_IP_BROKER", net);
```

4. **Sélectionner la carte** : Tools → Board → STM32L4 → B-L475E-IOT01A

5. **Uploader** le code

---

## 📱 Dashboard

Le dashboard est accessible à : **http://localhost:1880/ui**

### Page 1 : Weather (Vue d'Ensemble)

- 🌡️ **Jauge Température** : 0-50°C (jaune)
- 💧 **Jauge Humidité** : 0-100% (violet)
- 🌪️ **Jauge Pression** : 950-1050 mBar (rouge)
- 📷 Informations sur la carte et les concepteurs

### Page 2 : My Dashboard (Historique)

- 📊 Graphiques temporels pour Température, Humidité, Pression
- ⏱️ Période affichée : ~2-3 minutes
- 🔵 Courbes en temps réel (bleu cyan)

### Page 3 : Capteurs Inertiels

Grille 3×3 de graphiques :
- **Colonne 1** : Accéléromètre X/Y/Z
- **Colonne 2** : Magnétomètre X/Y/Z
- **Colonne 3** : Gyroscope X/Y/Z

---

## 🗄️ Base de Données

### Structure MongoDB

**Base** : `iot_sensors`  
**Collection** : `sensors_data`

### Schéma de Document

```json
{
  "_id": ObjectId("..."),
  "timestamp": ISODate("2026-01-04T19:15:26.000Z"),
  "sensor_type": "temperature",
  "topic": "/temperature",
  "value": 22.3,
  "unit": "°C",
}
```

---

## ⚠️ Problèmes et Solutions

### 1. Perte de connexion WiFi/MQTT

**Symptôme** : "Connection lost!" dans le moniteur série

**Solution** :
```cpp
if (!client.connected()) {
    client.disconnect();
    delay(5000);
    client.begin("192.168.0.135", net);
    if (client.connect("STM32-IOT", "user", "pass")) {
        Serial.println("Reconnected!");
        client.subscribe("/ihebz");
    }
}
```

✅ **Résultat** : Reconnexion automatique en 5-10 secondes

### 2. Surcharge du broker MQTT

**Symptôme** : Latence, messages perdus

**Solution** : Publication séquentielle (1 topic par seconde)
```cpp
if(topic==1) client.publish("/temperature", value);
if(topic==2) client.publish("/Humidite", value);
// ... cycle de 12 secondes
```

✅ **Résultat** : CPU < 5%, aucun message perdu

### 3. Configuration SPI WiFi

**Symptôme** : "WiFi module not present"

**Solution** :
```cpp
SPIClass SPI_3(PC12, PC11, PC10);
WiFiClass WiFi(&SPI_3, PE0, PE1, PE8, PB13);
```

✅ **Résultat** : Module détecté à chaque démarrage

### 4. Format des données MQTT

**Symptôme** : Valeurs incorrectes dans le dashboard

**Solution** :
```cpp
string_MQTT = String(sensor_value_T, 1); // 1 décimale
client.publish("/temperature", string_MQTT);
```

✅ **Résultat** : Données correctement formatées

---

## 🎥 Démonstration

### Vidéo Complète (5 minutes)
https://drive.google.com/file/d/1zKm94fT9ZjzvXOuhjBy3DmTO7Od-CmaY/view?usp=sharing

La vidéo de démonstration montre :

1. **Code Arduino** (45s) : IDE, code source, fonctions principales
2. **Connexion** (1min) : WiFi, MQTT, moniteur série
3. **Acquisition** (45s) : Valeurs en temps réel des 12 capteurs
4. **Node-RED** (45s) : 3 flows, nœuds actifs, MongoDB
5. **Dashboard** (1min15) : 3 pages, jauges, graphiques
6. **MongoDB** (30s) : Requêtes, documents, statistiques
7. **Test robustesse** (30s) : Déconnexion/reconnexion

### Commandes de Test

**Visualiser les messages MQTT** :
```bash
mosquitto_sub -h 192.168.0.135 -t "#" -v
```

---

## 🎓 Conclusion

### Objectifs Atteints

✅ **Acquisition multi-capteurs** : 6 capteurs, 12 valeurs, 1 Hz  
✅ **Communication MQTT** : Stable, reconnexion automatique  
✅ **Workflow Node-RED** : 3 flows, 50+ nœuds  
✅ **Dashboard interactif** : 3 pages, temps réel  
✅ **Stockage MongoDB** : Persistance, requêtes optimisées  
✅ **Code robuste** : Gestion d'erreurs, uptime 24h+  

### Compétences Acquises

- 💻 Programmation embarquée (STM32, C/C++)
- 📡 Protocoles IoT (MQTT, WiFi)
- 🔄 Orchestration de workflows (Node-RED)
- 🗄️ Bases de données NoSQL (MongoDB)
- 📊 Visualisation de données (Dashboard)
- 🐛 Debugging et résolution de problèmes

### Points Forts

- 🎯 Système complet end-to-end
- 🔒 Robuste et fiable
- 📈 Scalable et extensible
- 📱 Interface moderne et intuitive
- 📊 Données historiques pour analyse

---

## 🚀 Perspectives

### Court Terme (1-2 semaines)

- 📊 **Dashboard Grafana** : Graphiques avancés
- 📱 **Application mobile** : React Native / Flutter
- 🚨 **Système d'alertes** : Email/SMS automatiques
- 🔋 **Mode économie d'énergie** : Deep sleep STM32

### Moyen Terme (1-2 mois)

- 🔐 **Sécurité** : MQTTS (TLS), authentification JWT
- 📈 **InfluxDB** : Migration vers time-series database
- 🧠 **Machine Learning** : Détection d'anomalies
- 📍 **Géolocalisation** : GPS, multi-dispositifs

### Long Terme (6+ mois)

- 🌐 **Portail web** : Configuration sans code
- 🤖 **TinyML** : IA embarquée sur STM32
- ☁️ **Cloud IoT** : AWS IoT Core / Azure IoT Hub
- 🔗 **Blockchain** : Traçabilité immuable

---

## 📦 Structure du Dépôt

```
Projet_Reseaux_Locaux_Iheb-Zaouali_Iheb-Rahmeni_3AGE1/
├── README.md                    # Documentation complète
├── src/
│   ├── stm32_mqtt_sensors.ino  # Code Arduino
│   └── Readme
├── node-red/
│   ├── flows.json              # Export Node-RED
│   └── Readme
├── docs/
│   ├── images/                 # Captures d'écran
│   └── video/                  # Vidéo démo
└── config/
    ├── mosquitto.conf          # Config MQTT
    └── Readme
```

## 📞 Contact

**Auteurs** :  
- Iheb Zaouali : iheb.zaouali@etudiant-enit.utm.tn  
- Iheb Rahmeni : iheb.rahmeni@etudiant-enit.utm.tn

---

## 📄 Licence

Projet développé dans le cadre académique à l'ENIT.  
Utilisation libre pour fins éducatives et de recherche.

---

## 🙏 Remerciements

- Dr. Khaled Jelassi (encadrement)
- Communauté Arduino et Node-RED
- STMicroelectronics (BSP drivers)

---

## 📚 Références

- [STM32L4 Reference Manual](https://www.st.com/resource/en/reference_manual/dm00083560.pdf)
- [MQTT Protocol Specification](https://mqtt.org/mqtt-specification/)
- [Node-RED Documentation](https://nodered.org/docs/)
- [MongoDB Manual](https://docs.mongodb.com/manual/)

---

<div align="center">

**Développé avec ❤️ à l'ENIT - Janvier 2026**

[![ENIT](https://img.shields.io/badge/ENIT-Tunis-blue)](http://www.enit.rnu.tn/)
[![IoT](https://img.shields.io/badge/IoT-Project-green)]()
[![STM32](https://img.shields.io/badge/STM32-L475E-orange)]()






### 4️⃣ Configuration Arduino IDE

#### Télécharger Arduino IDE

1. Télécharger **Arduino IDE 2.x** (ou version 1.8.6+) depuis : https://www.arduino.cc/en/software
2. Installer Arduino IDE pour Windows (exécutable `.exe`)

#### Installer le support STM32

**Étape 1 : Ajouter l'URL du gestionnaire de cartes**

1. File → Preferences (ou `Ctrl + ,`)
2. Dans "Additional Boards Manager URLs", ajouter :
```
https://github.com/stm32duino/BoardManagerFiles/raw/master/package_stm_index.json
```
3. Cliquer sur "OK"

**Étape 2 : Installer le package STM32**

1. Tools → Board → Boards Manager
2. Dans la barre de recherche, taper : `STM32`
3. Installer **"STM32 MCU based boards" by STMicroelectronics**
4. Attendre la fin de l'installation

#### Installer les bibliothèques nécessaires

**Méthode 1 : Via le gestionnaire de bibliothèques (recommandé)**

1. Tools → Manage Libraries (ou `Ctrl + Shift + I`)
2. Installer les bibliothèques suivantes :

| Bibliothèque | Auteur | Description |
|--------------|--------|-------------|
| **WiFiST** | STMicroelectronics | Driver WiFi pour STM32 |
| **MQTT** | Joel Gaehwiler | Client MQTT |
| **STM32duino** | STMicroelectronics | Support capteurs IoT Node |

**Méthode 2 : Installation manuelle**

Si les bibliothèques ne sont pas disponibles via le gestionnaire :

- **WiFiST** : Incluse avec le BSP STM32
- **MQTT (arduino-mqtt)** : https://github.com/256dpi/arduino-mqtt
  - Télécharger le ZIP
  - Sketch → Include Library → Add .ZIP Library

#### Configurer la carte STM32L475E-IOT01A

**Sélectionner la carte** :
1. Tools → Board → STM32 boards groups → **B-L475E-IOT01A**

**Configurer les paramètres** :
- **Tools → Upload method** : STM32CubeProgrammer (SWD) ou Mass Storage
- **Tools → Port** : COMX (sélectionner le port USB de votre STM32)
- **Tools → USB support** : CDC (generic 'Serial' supersede U(S)ART)

#### Ouvrir et Configurer le projet

1. **Ouvrir le fichier** `src/stm32_mqtt_sensors.ino`

2. **Modifier les credentials WiFi** :
```cpp
char ssid[] = "VOTRE_SSID";        // Nom de votre réseau WiFi
char pass[] = "VOTRE_MOT_DE_PASSE"; // Mot de passe WiFi
```

3. **Modifier l'adresse du broker MQTT** :

Pour trouver l'IP de votre PC Windows :
```powershell
ipconfig
# Chercher "Adresse IPv4" de votre carte réseau active
# Exemple: 192.168.1.100
```

Dans le code Arduino :
```cpp
// Remplacer par l'IP de votre PC où Mosquitto est installé
client.begin("192.168.1.100", net);  // Port 1883 par défaut

// Ou utiliser un broker cloud public (pour tests)
// client.begin("broker.hivemq.com", net);
```

4. **Configuration des topics MQTT** :

Les topics utilisés dans le code :
```cpp
client.publish("/temperature", string_MQTT);
client.publish("/Humidite", string_MQTT);
client.publish("/Pression", string_MQTT);
client.publish("/Accelero_X", string_MQTT);
// ... etc pour les 12 capteurs
```

#### Initialisation SPI et WiFi (important)

Vérifier que ces lignes sont présentes au début du code :
```cpp
SPIClass SPI_3(PC12, PC11, PC10);
WiFiClass WiFi(&SPI_3, PE0, PE1, PE8, PB13);
```

#### Compiler et Uploader

1. **Vérifier le code** : Sketch → Verify/Compile (ou `Ctrl + R`)
2. **Uploader** : Sketch → Upload (ou `Ctrl + U`)
3. **Ouvrir le moniteur série** : Tools → Serial Monitor
   - **Baud rate** : 115200
   - Vous devriez voir les messages de connexion WiFi et MQTT

#### Vérification de l'upload

Dans le moniteur série (115200 baud), vous devriez voir :
```
OK
WIFI Module Initialized
Connected to WiFi
IP: 192.168.1.XXX
Connecting to MQTT...
MQTT connected!
Publishing: /temperature 22.5
Publishing: /Humidite 45.2
...
```

#### Dépannage Arduino IDE

**Problème : "WiFi module not present"**
- Vérifier la configuration SPI (lignes `SPIClass` et `WiFiClass`)
- Vérifier que la carte est bien sélectionnée

**Problème : Erreur de compilation**
- Vérifier que toutes les bibliothèques sont installées
- Tools → Board → Boards Manager → Réinstaller "STM32 MCU based boards"

**Problème : Port COM non visible**
- Installer le driver STLink : https://www.st.com/en/development-tools/stsw-link009.html
- Vérifier dans Gestionnaire de périphériques (Device Manager)

---

### 5️⃣ Test du Système Complet

#### Ordre de démarrage recommandé

1. ✅ **Mosquitto MQTT Broker** (service ou terminal)
   ```powershell
   net start mosquitto
   # OU en ligne de commande
   cd "C:\Program Files\mosquitto"
   mosquitto.exe -c mosquitto.conf -v
   ```

2. ✅ **Node-RED**
   ```powershell
   node-red
   # Attendre le message: Server now running at http://127.0.0.1:1880/
   ```

3. ✅ **MongoDB Atlas** (déjà en ligne - service cloud)

4. ✅ **STM32** 
   - Brancher la carte via USB
   - Uploader le code depuis Arduino IDE
   - Ouvrir le Serial Monitor (115200 baud)

#### Vérifications étape par étape

**1. Mosquitto fonctionne correctement** :
```powershell
# Vérifier que le port 1883 est en écoute
netstat -an | findstr 1883
# Doit afficher: TCP 0.0.0.0:1883 ... LISTENING
```

**Test MQTT en local** :
```powershell
# Terminal 1 - Subscribe
cd "C:\Program Files\mosquitto"
mosquitto_sub.exe -h localhost -t "#" -v

# Terminal 2 - Publish (dans un autre terminal)
cd "C:\Program Files\mosquitto"
mosquitto_pub.exe -h localhost -t "/test" -m "Hello"
```

**2. Node-RED fonctionne** :
- ✅ Ouvrir http://localhost:1880 (éditeur Node-RED)
- ✅ Ouvrir http://localhost:1880/ui (dashboard)
- ✅ Vérifier que tous les nœuds MQTT sont connectés (point vert sous les nœuds)
- ✅ Pas de messages d'erreur dans le panneau Debug

**Configuration des nœuds MQTT dans Node-RED** :
- Server : `localhost` ou `127.0.0.1`
- Port : `1883`
- Topics : `/temperature`, `/Humidite`, `/Pression`, etc.

**3. STM32 connecté et fonctionnel** :

Ouvrir le **Serial Monitor** dans Arduino IDE (Tools → Serial Monitor, 115200 baud).

Séquence de démarrage attendue :
```
OK
WIFI Module Initialized
es-wifi module MAC Address: XX:XX:XX:XX:XX:XX
Connected to SSID: VotreSsid
IP Address: 192.168.1.XXX
Connecting to MQTT broker at 192.168.1.100:1883...
MQTT connected!

Publishing: /temperature 22.5
Publishing: /Humidite 45.3
Publishing: /Pression 1013.2
Publishing: /Accelero_X 12
...
```

**4. Données reçues dans Node-RED** :

Dans Node-RED, aller dans le panneau **Debug** (icône insecte à droite).
Vous devriez voir les messages MQTT arriver :
```
/temperature : 22.5
/Humidite : 45.3
/Pression : 1013.2
/Accelero_X : 12
...
```

**5. Dashboard affiche les données** :

Ouvrir http://localhost:1880/ui

Vérifier :
- ✅ Page "Weather" : Jauges de température, humidité, pression se mettent à jour
- ✅ Page "My Dashboard" : Graphiques temps réel affichent les courbes
- ✅ Page "Capteurs Inertiels" : Données d'accéléromètre, gyroscope, magnétomètre

**6. Données dans MongoDB Atlas** :

1. Aller sur https://cloud.mongodb.com
2. Se connecter à votre compte
3. Clusters → Browse Collections
4. Sélectionner : `iot_sensors` → `sensor_data`
5. Vérifier la présence de documents récents avec timestamp actuel

Exemple de document :
```json
{
  "_id": ObjectId("..."),
  "timestamp": ISODate("2026-01-05T10:30:00.000Z"),
  "sensor_type": "temperature",
  "topic": "/temperature",
  "value": 22.5,
  "unit": "°C",
  "device_id": "STM32-B-L475-IOT01A2"
}
```
</div>
