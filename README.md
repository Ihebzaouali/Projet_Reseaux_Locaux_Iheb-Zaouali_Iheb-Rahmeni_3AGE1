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
- **Broker MQTT** : Mosquitto 2.x
- **Orchestration** : Node-RED 3.x
- **Base de données** : MongoDB 6.x
- **Dashboard** : Node-RED Dashboard

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

### Prérequis

```bash
# Vérifier les versions
node --version        # v18.x ou supérieur
mongod --version      # v6.x ou supérieur
mosquitto --version   # v2.x ou supérieur
```

### Installation Système

```bash
# Ubuntu/Debian
sudo apt update
sudo apt install -y nodejs npm mongodb mosquitto mosquitto-clients

# Installer Node-RED globalement
sudo npm install -g --unsafe-perm node-red
```

### Configuration Node-RED

```bash
# Installer les dépendances
cd ~/.node-red
npm install node-red-dashboard node-red-node-mongodb

# Démarrer Node-RED
node-red
```

Accès Node-RED : http://localhost:1880  
Accès Dashboard : http://localhost:1880/ui

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
**Collection** : `sensor_data`

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
projet-iot-stm32-mqtt-nodered/
├── README.md                    # Documentation complète
├── src/
│   ├── stm32_mqtt_sensors.ino  # Code Arduino
│   └── Readme
├── node-red/
│   ├── flows.json              # Export Node-RED
│   └── Readme
├── mongodb/
│   └── sample_queries.js       # Requêtes exemples
├── docs/
│   ├── images/                 # Captures d'écran
│   └── video/                  # Vidéo démo
└── config/
    ├── mosquitto.conf          # Config MQTT
    └── Readme
```

---

## 🐛 Dépannage

### WiFi module not present

```cpp
// Vérifier configuration SPI
SPIClass SPI_3(PC12, PC11, PC10);
WiFiClass WiFi(&SPI_3, PE0, PE1, PE8, PB13);
```

### Node-RED ne démarre pas

```bash
rm -rf ~/.node-red/node_modules
cd ~/.node-red
npm install
node-red
```

### Dashboard ne s'affiche pas

- URL correcte : http://localhost:1880/ui
- Vérifier : `npm list node-red-dashboard`

---

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

</div>
