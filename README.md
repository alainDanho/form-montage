# 📋 Formulaire de Collecte de Données de Montage - RTI

Ce projet a pour objectif de faciliter la collecte trimestrielle des données de montage des collaborateurs du service **Montage et Planification** du groupe **ETI (Radiodiffusion Télévision Ivoirienne)**.

Il s'agit d'un formulaire web léger qui envoie les données directement dans un Google Sheet, sans nécessiter de serveur ni de base de données complexe.

## 🏗️ Architecture du Projet

Le projet repose sur une architecture "serverless" gratuite et simple :

1. **Frontend (Interface)** : Un fichier unique `index.html` (HTML, CSS et JavaScript) hébergé gratuitement sur **GitHub Pages**.
2. **Backend (Traitement)** : Un script **Google Apps Script** déployé en tant qu'application web qui reçoit les données.
3. **Base de données (Stockage)** : Un **Google Sheets** où les données sont ajoutées automatiquement ligne par ligne.

## 🚀 Fonctionnalités

- Formulaire dynamique : possibilité d'ajouter plusieurs éléments montés dans une même soumission.
- Saisie de la durée précise (Heures, Minutes, Secondes).
- Liste déroulante pour le type d'élément (`Reportage JT`, `Émission TV`, `Documentaire`, `Fiction`).
- Envoi sécurisé des données via `fetch` API.
- Enregistrement automatique avec horodatage (Timestamp) dans le Google Sheet.

## 🛠️ Guide d'installation et de configuration

### 1. Configuration du Google Sheet
Créez un Google Sheet nommé par exemple `Montage trimestriel - RTI` et ajoutez les en-têtes suivants dans la première ligne :
- `Timestamp`
- `Nom_du_monteur`
- `Trimestre`
- `Annee`
- `Titre_element`
- `Duree`
- `Type_element`
- `Observations`

### 2. Configuration de Google Apps Script
1. Dans votre Google Sheet, allez dans `Extensions > Apps Script`.
2. Collez le code backend (disponible dans le script du projet).
3. Exécutez la fonction `initialSetup` **une seule fois** et autorisez le script.
4. Déployez le script : `Déployer > Nouveau déploiement > Application web`.
   - Exécuter en tant que : **Moi-même**
   - Qui a accès : **Tout le monde**
5. Copiez l'**URL de l'application web** générée.

### 3. Configuration du Frontend
Ouvrez le fichier `index.html` et remplacez la ligne suivante par l'URL copiée à l'étape précédente :
```javascript
const SCRIPT_URL = 'https://script.google.com/macros/s/AKfycbztR7Tj_Ox2NbMmEGLFQEq38TMTJdbl2eTGRoEu0cxVoHovGb0KwCy4-DmnGp6W9w/exec';
