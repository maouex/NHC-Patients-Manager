# 🔄 Système de Mise à Jour Automatique

Ce document explique comment fonctionne le système de mise à jour automatique de l'application Presta Patients Manager.

## 📋 Vue d'ensemble

Le système de mise à jour permet à l'application de :
- Détecter automatiquement les nouvelles versions publiées sur GitHub
- Télécharger et installer les mises à jour en un clic
- Préserver toutes vos données lors de la mise à jour
- **Gérer les changements de nom de fichier** (ex: v1.0.html → v2.0.html)

## 🎯 Architecture

### Fichier `version.json`

Le fichier `version.json` est le cœur du système. Il contient les métadonnées de version :

```json
{
  "version": "1.0.0",
  "fileName": "Presta-Patients-Manager-v1.0.html",
  "downloadUrl": "https://raw.githubusercontent.com/username/repo/main/Presta-Patients-Manager-v1.0.html",
  "releaseDate": "2025-01-13",
  "releaseNotes": {
    "fr": [
      "✨ Première version stable",
      "🔧 Nouvelle fonctionnalité X",
      "🐛 Correction du bug Y"
    ]
  },
  "minVersion": "1.0.0",
  "checksum": ""
}
```

### Pourquoi `version.json` ?

**Avantages :**
1. ✅ **Changement de nom transparent** : Le fichier HTML peut changer de nom sans casser le système
2. ✅ **Métadonnées riches** : Notes de version, date de publication, etc.
3. ✅ **URL stable** : Le fichier `version.json` reste toujours au même endroit
4. ✅ **Rétrocompatibilité** : L'ancienne méthode (URL directe du HTML) fonctionne toujours

## 🚀 Configuration

### Méthode 1 : Via version.json (Recommandée)

1. **Pousser le fichier `version.json` sur la branche `main`** de votre dépôt GitHub

2. **Dans l'application**, aller dans **Mise à jour** → **Configuration**

3. **Configurer l'URL** :
   ```
   https://raw.githubusercontent.com/maouex/Presta-Patients-Manager/main/version.json
   ```

4. **Activer** "Vérifier automatiquement les mises à jour au démarrage"

5. **Enregistrer**

### Méthode 2 : URL directe (Legacy)

Si vous préférez l'ancienne méthode, vous pouvez toujours utiliser l'URL directe du fichier HTML :
```
https://raw.githubusercontent.com/username/repo/main/Presta-Patients-Manager.html
```

⚠️ **Limitation** : Si vous renommez le fichier HTML, vous devrez reconfigurer l'URL.

## 📝 Workflow de Publication

### 1. Préparer une nouvelle version

#### a. Mettre à jour la version dans le fichier HTML

Modifier la constante `APP_VERSION` :
```javascript
const APP_VERSION = '1.1.0'; // Anciennement '1.0.0'
```

#### b. Renommer le fichier (optionnel)

Si vous voulez changer le nom :
```
Presta-Patients-Manager-v1.0.html → Presta-Patients-Manager-v1.1.html
```

#### c. Mettre à jour `version.json`

```json
{
  "version": "1.1.0",
  "fileName": "Presta-Patients-Manager-v1.1.html",
  "downloadUrl": "https://raw.githubusercontent.com/maouex/Presta-Patients-Manager/main/Presta-Patients-Manager-v1.1.html",
  "releaseDate": "2025-01-15",
  "releaseNotes": {
    "fr": [
      "✨ Ajout du filtre de patients archivés",
      "🐛 Correction du bug d'affichage",
      "⚡ Amélioration des performances"
    ]
  }
}
```

### 2. Pousser sur `main`

```bash
git add .
git commit -m "🚀 Version 1.1.0"
git push origin main
```

### 3. Les utilisateurs sont notifiés

Dès que vous poussez sur `main` :
1. Les utilisateurs avec "vérification automatique" verront une notification au démarrage
2. Les autres peuvent cliquer sur "Vérifier les mises à jour"
3. L'application détecte la nouvelle version **même si le nom a changé**
4. Un clic pour télécharger et installer

## 🔒 Sécurité et Données

- ✅ Toutes les données utilisateur sont préservées (localStorage)
- ✅ Backup automatique avant installation
- ✅ Historique des mises à jour conservé
- ✅ Possibilité de ne pas installer si refus

## 🎨 Versioning Sémantique

Le système utilise le versioning sémantique (semver) :

```
MAJEUR.MINEUR.PATCH
  1   .  0   .  0
```

- **MAJEUR** : Changements incompatibles
- **MINEUR** : Nouvelles fonctionnalités rétrocompatibles
- **PATCH** : Corrections de bugs

**Exemples :**
- `1.0.0` → `1.0.1` : Correction de bug
- `1.0.0` → `1.1.0` : Nouvelle fonctionnalité
- `1.0.0` → `2.0.0` : Changement majeur

## 📊 Exemple de Migration v1 → v2

### Avant (v1.0.0)
- Fichier : `Presta-Patients-Manager-v1.0.html`
- URL configurée : `...main/Presta-Patients-Manager-v1.0.html`

### Après (v2.0.0)
1. Créer `Presta-Patients-Manager-v2.0.html`
2. Mettre à jour `version.json` :
   ```json
   {
     "version": "2.0.0",
     "fileName": "Presta-Patients-Manager-v2.0.html",
     "downloadUrl": "https://raw.githubusercontent.com/.../Presta-Patients-Manager-v2.0.html",
     ...
   }
   ```
3. Pousser sur `main`
4. ✅ Les utilisateurs détectent automatiquement la v2.0.0 !

## 🛠️ Dépannage

### L'application ne détecte pas les mises à jour

1. Vérifier que `version.json` est sur la branche `main`
2. Vérifier l'URL RAW configurée
3. Vérifier que la version dans `version.json` est supérieure à `APP_VERSION`
4. Vider le cache du navigateur (Ctrl+F5)

### Erreur "Fichier version.json invalide"

Vérifier que le JSON est valide :
- `version` doit être présent
- `downloadUrl` doit être présent
- Format semver correct (X.Y.Z)

### L'URL du fichier HTML ne fonctionne pas

Vérifier que l'URL est correcte :
- Utiliser l'URL **RAW** de GitHub
- Format : `https://raw.githubusercontent.com/user/repo/branch/file.html`
- Encoder les espaces avec `%20` si nécessaire

## 📚 Ressources

- [Versioning Sémantique](https://semver.org/lang/fr/)
- [GitHub RAW URLs](https://docs.github.com/en/repositories/working-with-files/using-files/getting-permanent-links-to-files)
