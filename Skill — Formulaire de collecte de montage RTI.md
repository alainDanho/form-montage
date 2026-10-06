---
name: formulaire-montage-rti
description: Skill pour déployer et maintenir le formulaire de collecte trimestrielle des données de montage de la RTI (Groupe ETI). Couvre la création du Google Sheet, Apps Script, formulaire HTML, hébergement GitHub Pages, et résolution des problèmes courants.
---

# 📘 Skill — Formulaire de collecte de montage RTI

## 🎯 Objectif
Permettre aux monteurs du service **Montage et Planification** de la RTI de saisir trimestriellement :
- Leur nom
- Le trimestre et l’année
- Les titres des éléments montés
- La durée de chaque élément (heures, minutes, secondes)
- Le type d’élément
- Des observations

Les données sont enregistrées **automatiquement** dans un Google Sheet, sans intervention manuelle.

---

## 🏗️ Architecture technique
| Composant | Rôle | Outil |
|---|---|---|
| **Frontend** | Formulaire visible par les monteurs | HTML/CSS/JS hébergé sur **GitHub Pages** |
| **Backend** | Réception et écriture des données | **Google Apps Script** (Web App) |
| **Base de données** | Stockage des données | **Google Sheets** |

Flux : `Formulaire → Apps Script → Google Sheet`

---

## ✅ Étapes de mise en place

### 1. Création du Google Sheet
Créer une feuille avec les en-têtes suivants (première ligne) :
`Timestamp`, `Nom_du_monteur`, `Trimestre`, `Annee`, `Titre_element`, `Duree`, `Type_element`, `Observations`.

### 2. Configuration de Google Apps Script
1. Dans le Google Sheet : `Extensions > Apps Script`.
2. Coller le code backend (`initialSetup`, `doPost`).
3. Exécuter `initialSetup` une seule fois et autoriser le script.
4. Déployer : `Déployer > Nouveau déploiement > Application web`.
   - Exécuter en tant que : **Moi-même**
   - Qui a accès : **Tout le monde**
5. Copier l’URL de l’application web.

### 3. Création du formulaire HTML (`index.html`)
- Champs : nom, trimestre, année, titre, durée (HH/MM/SS), type, observations.
- Bouton **Ajouter un élément** pour saisir plusieurs lignes.
- Envoi via `fetch()` vers l’URL Apps Script.
- Affichage d’un message de succès/erreur.

### 4. Hébergement sur GitHub Pages
- Dépôt public : `alainDanho/form-montage`
- Fichier `index.html` à la racine.
- Activation dans `Settings > Pages` : branche `main`, dossier `/ (root)`.
- URL publique générée :  
  👉 `https://alaindanho.github.io/form-montage/`

### 5. Personnalisation du formulaire
- En-tête : Groupe RTI, Direction de la production et de la Fiction, Service Montage et Planification.
- Liste `Type_element` : Reportage, Débat, Magazine, Documentaire, Fiction.
- Champ `Trimestre` : liste complète avec **T3 pré-sélectionné** (`selected`).

---

## ⚠️ Problèmes rencontrés et solutions

| Problème | Cause | Solution |
|---|---|---|
| Bouton « Add file » absent sur GitHub | Dépôt vide sans commit | Cliquer sur **« uploading an existing file »** |
| Autorisation Apps Script ratée | Fenêtre fermée trop vite | Réexécuter `initialSetup` ou révoquer l’accès dans les paramètres Google |
| Accès Web App non configuré | Option « Tout le monde » oubliée | Modifier le déploiement via **Gérer les déploiements** |
| Modifications non visibles | Cache navigateur | `Ctrl + F5` ou navigation privée |
| Déploiement GitHub Pages bloqué | File d’attente Actions saturée | Annuler le workflow bloqué et refaire un commit |

---

## 📌 État actuel du projet
- ✅ Google Sheet créé et prêt.
- ✅ Script Apps Script déployé (URL récupérée).
- ✅ Formulaire HTML fonctionnel, personnalisé et lié au script.
- ✅ Dépôt GitHub créé, fichier `index.html` uploadé.
- ⏳ **GitHub Pages** : le dernier déploiement n’est pas encore passé au vert après 7 minutes.
  - Action recommandée : annuler le workflow bloqué dans **Actions**, puis refaire un petit commit pour relancer le déploiement.

---

## 🚀 Prochaines étapes
1. **Débloquer GitHub Pages** :
   - Aller dans `Actions` → annuler le job bloqué (`Cancel workflow`).
   - Faire une modification mineure dans `index.html` → `Commit changes`.
   - Attendre la coche verte ✅.
2. **Tester le formulaire** :
   - Ouvrir `https://alaindanho.github.io/form-montage/`
   - Remplir et envoyer.
   - Vérifier l’arrivée des données dans le Google Sheet.
3. **Partager le lien** avec les monteurs (email, WhatsApp, QR code).
4. **Documenter** : le fichier `README.md` peut être ajouté au dépôt pour référence.

---

## 💡 Bonnes pratiques
- Les noms des champs HTML doivent être **identiques** aux en-têtes du Google Sheet.
- Toujours vérifier l’onglet **Actions** après un commit sur GitHub.
- Vider le cache (`Ctrl + F5`) après chaque mise à jour du formulaire.
- Ne pas renommer la branche `main` sans raison (risque de casser GitHub Pages).

---

## 🧰 Checklist rapide

- [ ] Google Sheet créé avec les bons en-têtes
- [ ] Script Apps Script déployé et autorisé
- [ ] URL Apps Script copiée dans `index.html`
- [ ] Fichier `index.html` uploadé sur GitHub
- [ ] GitHub Pages activé (`main` + `/root`)
- [ ] Déploiement Actions au vert ✅
- [ ] Formulaire testé et données visibles dans le Sheet
- [ ] Lien partagé avec les monteurs