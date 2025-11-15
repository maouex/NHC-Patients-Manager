# 🎨 Mockup Dashboard Multi-Vues - NHC Patients Manager

## 📐 Architecture Globale

```
┌─────────────────────────────────────────────────────────────────────────────┐
│ TOP NAVBAR (Fixe, 64px height)                                              │
│ [Logo NPM] [Recherche Globale........] [Notifications] [Profil] [Theme]    │
└─────────────────────────────────────────────────────────────────────────────┘
┌────────┬──────────────────────────────────────────────────────┬─────────────┐
│        │                                                      │   PANEL     │
│ SIDE   │         ZONE PRINCIPALE (Dashboard)                 │   LATERAL   │
│ MENU   │                                                      │  (Coulisse) │
│        │                                                      │             │
│ 240px  │              Widgets modulaires                      │    400px    │
│        │                                                      │   (optionel)│
│        │                                                      │             │
└────────┴──────────────────────────────────────────────────────┴─────────────┘
```

---

## 🎯 Zone 1 : TOP NAVBAR

### Design
```
┌─────────────────────────────────────────────────────────────────────┐
│  🏥 NPM  │ 🔍 Rechercher patient, ordonnance...  │ 🔔³ │ 👤 │ 🌙 │
│          │     [Ctrl+K pour ouvrir]             │     │ Dr │    │
└─────────────────────────────────────────────────────────────────────┘
```

**Éléments :**
- **Logo** : Gradient circulaire + NPM (cliquable → retour dashboard)
- **Barre de recherche universelle** :
  - Auto-complete intelligent
  - Recherche multi-critères (nom, NSS, date, statut)
  - Résultats groupés par type (Patients, Ordonnances, Archives)
  - Raccourci Ctrl+K pour focus
  - Icon de filtre à droite pour recherche avancée

- **Notifications** (Badge avec compteur) :
  - Dropdown au clic
  - Liste notifications avec avatar + message + temps
  - Categories : Urgences (rouge), Renouvellements (orange), Info (bleu)
  - "Tout marquer comme lu" en footer

- **Profil** :
  - Avatar + Initiales
  - Dropdown : Mon compte, Paramètres, Déconnexion

- **Toggle Theme** :
  - Icon soleil/lune
  - Switch smooth entre light/dark/auto

**Style :**
- Background : Blanc (light) / #0F172A (dark)
- Ombre portée légère (shadow-sm)
- Border bottom subtile
- Sticky top position

---

## 🎯 Zone 2 : SIDEBAR MENU (Gauche)

### Design
```
┌──────────────────────┐
│                      │
│  📊 VUE D'ENSEMBLE   │ ← Section active
│  ├─ Dashboard        │
│  └─ Analytics        │
│                      │
│  👥 PATIENTS         │
│  ├─ Tous             │
│  ├─ Actifs (245)     │
│  ├─ Inactifs         │
│  └─ Archives         │
│                      │
│  📋 ORDONNANCES      │
│  ├─ Toutes           │
│  ├─ Valides (189)    │
│  ├─ À renouveler (12)│ ← Badge orange
│  └─ Expirées         │
│                      │
│  📅 CALENDRIER       │
│                      │
│  📈 RAPPORTS         │
│                      │
│  ⚙️ PARAMÈTRES       │
│                      │
│ ─────────────────    │
│  💾 Export           │
│  📥 Import           │
└──────────────────────┘
```

**Fonctionnalités :**
- **Sections collapsibles** : Caret icon pour expand/collapse
- **Badges de compteur** : Affichage dynamique du nombre d'items
- **Badges d'alerte** : Orange/rouge pour urgences
- **Icons** : SVG moderne (Lucide icons recommandé)
- **Active state** :
  - Background gradient bleu subtil
  - Border left 3px solid #3B82F6
  - Icon + texte en gras

**Interactions :**
- Hover : Background gris très léger + cursor pointer
- Click : Navigation instantanée avec fade transition
- Bouton toggle en bas pour réduire (icon only mode)

**Style :**
- Background : #F8FAFC (light) / #1E293B (dark)
- Largeur : 240px (expandé) / 80px (réduit)
- Padding : 16px
- Border right subtile

---

## 🎯 Zone 3 : DASHBOARD PRINCIPAL

### Layout Global (Grid Modulaire)

```
┌─────────────────────────────────────────────────────────────────┐
│ 📍 Breadcrumb : Accueil > Dashboard                             │
│ ─────────────────────────────────────────────────────────────   │
│                                                                  │
│ ┌──────────── KPI CARDS (4 colonnes) ─────────────────┐        │
│ │ [KPI 1]    [KPI 2]    [KPI 3]    [KPI 4]            │        │
│ └─────────────────────────────────────────────────────┘        │
│                                                                  │
│ ┌─────────────┬─────────────────────────────────────┐          │
│ │   WIDGET    │      WIDGET PRINCIPAL               │          │
│ │   GAUCHE    │   (Chart/Graphique/Table)           │          │
│ │             │                                     │          │
│ │   (33%)     │         (67%)                       │          │
│ └─────────────┴─────────────────────────────────────┘          │
│                                                                  │
│ ┌─────────────────────────────────────────────────────┐        │
│ │      WIDGET PLEINE LARGEUR                          │        │
│ │      (Timeline / Liste patients)                    │        │
│ └─────────────────────────────────────────────────────┘        │
│                                                                  │
│ ┌─────────────┬─────────────┬─────────────┐                   │
│ │  WIDGET 1   │  WIDGET 2   │  WIDGET 3   │                   │
│ │  (33%)      │  (33%)      │  (33%)      │                   │
│ └─────────────┴─────────────┴─────────────┘                   │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

### Widgets Détaillés

#### 🔢 **KPI Cards** (Rangée supérieure)

```
┌──────────────────────────────┐  ┌──────────────────────────────┐
│ 👥 Patients Actifs           │  │ 📋 Ordonnances               │
│                              │  │                              │
│      245                     │  │      189                     │
│      ↗ +12 ce mois          │  │      ↗ +8 cette semaine     │
│                              │  │                              │
│ ▁▂▃▅▆▇█ Mini chart          │  │ ▁▃▂▅▆▇▅ Mini chart          │
└──────────────────────────────┘  └──────────────────────────────┘

┌──────────────────────────────┐  ┌──────────────────────────────┐
│ ⚠️ À Renouveler              │  │ 📊 Taux de Renouvellement   │
│                              │  │                              │
│      12                      │  │      94.2%                   │
│      ⚠️ 3 urgents           │  │      ↗ +2.1% vs mois dernier│
│                              │  │                              │
│ [Voir liste]                 │  │ ████████░░ Progress bar      │
└──────────────────────────────┘  └──────────────────────────────┘
```

**Design :**
- Background : Blanc avec gradient subtil en overlay
- Border top 4px coloré selon le type (bleu, vert, orange, violet)
- Ombre douce au hover (translateY -2px)
- Icon en haut gauche avec background circular coloré
- Chiffre principal : Grande typo (32-40px) en gradient
- Sous-texte : Variation avec arrow et couleur (vert = positif, rouge = négatif)
- Mini chart : Sparkline SVG animé
- Height : 140px

---

#### 📊 **Widget : Statistiques Ordonnances** (Graphique)

```
┌───────────────────────────────────────────────────────────┐
│ 📊 Évolution des Ordonnances (6 derniers mois)            │
│ [Ligne] [Barre] [Aire]  •••  [Export CSV] [Fullscreen]   │
│                                                            │
│  300│                                        ●             │
│     │                                   ●                  │
│  200│                              ●                       │
│     │                         ●                            │
│  100│                    ●                                 │
│     │               ●                                      │
│    0└────┴────┴────┴────┴────┴────┴────                   │
│      Jan  Fev  Mar  Avr  Mai  Jun                         │
│                                                            │
│  ● Ordonnances créées  ● Renouvelées  ● Expirées         │
└───────────────────────────────────────────────────────────┘
```

**Features :**
- Tabs pour changer type de graphique (Ligne/Barre/Aire)
- Tooltip au hover sur les points
- Légende interactive (cliquer pour masquer/afficher série)
- Export en CSV/PNG
- Fullscreen mode
- Zoom & Pan (molette)
- Animations au chargement

**Library suggestion :** Chart.js ou Apache ECharts

---

#### 📅 **Widget : Calendrier Renouvellements**

```
┌────────────────────────────────────────────┐
│ 📅 Renouvellements à venir (30 prochains j)│
│                                             │
│  Lun 15 Nov                                │
│  ┌─────────────────────────────────────┐   │
│  │ 🟢 Dupont Jean - NSS 1234567        │   │
│  │    💊 Doliprane - Expire dans 2j    │   │
│  │    [📋 Voir] [🔄 Renouveler]        │   │
│  └─────────────────────────────────────┘   │
│                                             │
│  Mar 16 Nov                                │
│  ┌─────────────────────────────────────┐   │
│  │ 🟡 Martin Claire - NSS 7654321      │   │
│  │    💊 Antibio - Expire dans 3j      │   │
│  │    [📋 Voir] [🔄 Renouveler]        │   │
│  └─────────────────────────────────────┘   │
│                                             │
│  Mer 17 Nov                                │
│  ┌─────────────────────────────────────┐   │
│  │ 🔴 Durand Paul - NSS 9876543        │   │
│  │    💊 Insuline - Expire demain! ⚠️  │   │
│  │    [📋 Voir] [🔄 Renouveler]        │   │
│  └─────────────────────────────────────┘   │
│                                             │
│         [Voir tous les renouvellements]    │
└────────────────────────────────────────────┘
```

**Design :**
- Timeline verticale avec dates sticky
- Cards patients avec couleur status (vert/orange/rouge)
- Actions rapides inline
- Scroll vertical si beaucoup d'items
- Badge urgence clignotant pour les critiques

---

#### 👥 **Widget : Patients Récents**

```
┌─────────────────────────────────────────────────────────┐
│ 👥 Patients Récents                    [Filtrer ▼]      │
│                                                          │
│ Nom             NSS         Dernière visite    Actions  │
│ ─────────────────────────────────────────────────────   │
│ 🟢 Dupont J.    123****     15/11/2025 14:30   [👁][✏️]│
│ 🟢 Martin C.    765****     14/11/2025 09:15   [👁][✏️]│
│ 🟡 Durand P.    987****     12/11/2025 16:45   [👁][✏️]│
│ 🔴 Bernard M.   456****     10/11/2025 11:20   [👁][✏️]│
│ 🟢 Petit L.     321****     09/11/2025 13:00   [👁][✏️]│
│                                                          │
│ Affiche 5 sur 245 patients  [Voir tout →]              │
└─────────────────────────────────────────────────────────┘
```

**Features :**
- Table responsive avec tri au clic sur headers
- Status coloré (vert = actif, orange = attention, rouge = urgent)
- NSS masqué partiellement (privacy)
- Actions rapides : Voir détails (👁) / Éditer (✏️)
- Pagination ou infinite scroll
- Filtre rapide par status

---

#### 🔥 **Widget : Quick Actions**

```
┌────────────────────────────────────────┐
│ ⚡ Actions Rapides                     │
│                                         │
│ ┌────────────┐  ┌────────────┐        │
│ │   👤 +     │  │   📋 +     │        │
│ │  Nouveau   │  │  Nouvelle  │        │
│ │  Patient   │  │ Ordonnance │        │
│ └────────────┘  └────────────┘        │
│                                         │
│ ┌────────────┐  ┌────────────┐        │
│ │   📥       │  │   📊       │        │
│ │  Import    │  │  Générer   │        │
│ │  Données   │  │  Rapport   │        │
│ └────────────┘  └────────────┘        │
└────────────────────────────────────────┘
```

**Design :**
- Grid 2x2
- Cards cliquables avec hover effect (scale 1.05)
- Icon + Label centré
- Gradient background différent par action
- Click → Ouvre modal ou panel lateral

---

#### 📈 **Widget : Statistiques Temps Réel**

```
┌───────────────────────────────────────┐
│ 📈 Activité Temps Réel                │
│                                        │
│ Aujourd'hui (15 Nov 2025)             │
│                                        │
│ ✅ 8 ordonnances créées               │
│ 🔄 12 renouvellements                 │
│ 👥 3 nouveaux patients                │
│ 📥 1 import effectué                  │
│                                        │
│ ▁▂▃▅▆▇█▇▆▅▃▂▁ Activité journée       │
│                                        │
│ 🔴 Live : Dernière action il y a 2min │
└───────────────────────────────────────┘
```

**Features :**
- Auto-refresh toutes les 30 secondes
- Badge "Live" pulsant
- Mini chart activité horaire
- Liste actions récentes avec timestamp

---

## 🎯 Zone 4 : PANEL LATERAL (Droite, Coulissant)

### Design Fermé
```
│ >  │  ← Bouton toggle (30px width)
```

### Design Ouvert (400px)
```
┌─────────────────────────────────────────┐
│ < Détails Patient              [✕]      │
│ ──────────────────────────────────────  │
│                                          │
│ ┌─────────────────────────────────────┐ │
│ │     [Photo]                         │ │
│ │                                     │ │
│ │  Jean DUPONT                        │ │
│ │  🟢 Actif                           │ │
│ │                                     │ │
│ │  📞 06 12 34 56 78                  │ │
│ │  📧 j.dupont@email.com              │ │
│ │  📍 15 rue de Paris, 75001          │ │
│ └─────────────────────────────────────┘ │
│                                          │
│ 📋 ORDONNANCES (3)                      │
│ ┌─────────────────────────────────────┐ │
│ │ 💊 Doliprane 1000mg                 │ │
│ │    Expire: 17/11/2025 ⚠️            │ │
│ │    [Renouveler]                     │ │
│ └─────────────────────────────────────┘ │
│                                          │
│ ┌─────────────────────────────────────┐ │
│ │ 💊 Amoxicilline 500mg               │ │
│ │    Expire: 25/12/2025 ✅            │ │
│ │    [Voir détails]                   │ │
│ └─────────────────────────────────────┘ │
│                                          │
│ 📅 HISTORIQUE                           │
│ ┌─────────────────────────────────────┐ │
│ │ • 15/11/2025 - Consultation         │ │
│ │ • 12/11/2025 - Renouvellement       │ │
│ │ • 05/11/2025 - Nouvelle ordonnance  │ │
│ └─────────────────────────────────────┘ │
│                                          │
│ [✏️ Modifier] [🗑️ Archiver]            │
│                                          │
└─────────────────────────────────────────┘
```

**Fonctionnalités :**
- **Slide-in animation** depuis la droite (300ms ease-out)
- **Overlay backdrop** semi-transparent au clic ferme le panel
- **Contexte dynamique** : Affiche détails selon ce qui est cliqué (patient, ordonnance, etc.)
- **Scroll interne** si contenu long
- **Actions rapides** en footer sticky
- **Tabs** en haut si plusieurs vues (Infos / Ordonnances / Historique)

**Triggers :**
- Clic sur ligne tableau → Ouvre détails patient
- Clic sur KPI card → Ouvre détails statistiques
- Clic sur notification → Ouvre détails item

---

## 🎨 Système de Design Tokens

### Couleurs Proposées (Palette Professionnelle)

**Light Mode :**
```css
--color-primary: #2563EB      /* Bleu principal */
--color-primary-light: #60A5FA
--color-primary-dark: #1E40AF

--color-success: #10B981      /* Vert */
--color-warning: #F59E0B      /* Orange */
--color-danger: #EF4444       /* Rouge */
--color-info: #06B6D4         /* Cyan */

--color-bg-primary: #FFFFFF
--color-bg-secondary: #F8FAFC
--color-bg-tertiary: #F1F5F9

--color-text-primary: #0F172A
--color-text-secondary: #64748B
--color-text-muted: #94A3B8

--color-border: #E2E8F0
--color-border-light: #F1F5F9
```

**Dark Mode :**
```css
--color-bg-primary: #0F172A
--color-bg-secondary: #1E293B
--color-bg-tertiary: #334155

--color-text-primary: #F8FAFC
--color-text-secondary: #CBD5E1
--color-text-muted: #94A3B8
```

### Spacing System
```css
--spacing-xs: 4px
--spacing-sm: 8px
--spacing-md: 16px
--spacing-lg: 24px
--spacing-xl: 32px
--spacing-2xl: 48px
```

### Typography
```css
--font-family: 'Inter', system-ui, sans-serif
--font-size-xs: 12px
--font-size-sm: 14px
--font-size-base: 16px
--font-size-lg: 18px
--font-size-xl: 20px
--font-size-2xl: 24px
--font-size-3xl: 32px
```

### Shadows
```css
--shadow-sm: 0 1px 2px rgba(0,0,0,0.05)
--shadow-md: 0 4px 6px rgba(0,0,0,0.07)
--shadow-lg: 0 10px 15px rgba(0,0,0,0.1)
--shadow-xl: 0 20px 25px rgba(0,0,0,0.15)
```

### Border Radius
```css
--radius-sm: 6px
--radius-md: 8px
--radius-lg: 12px
--radius-xl: 16px
--radius-full: 9999px
```

---

## 🎬 Interactions & Animations

### Transitions
- **Navigation** : 200ms ease-in-out
- **Panel slide** : 300ms cubic-bezier(0.4, 0, 0.2, 1)
- **Modal** : Scale from 0.95 to 1 + fade (250ms)
- **Hover effects** : 150ms ease

### Micro-interactions
- **KPI Cards** : Hover → translateY(-4px) + shadow lift
- **Buttons** : Hover → Slight brightness increase + shadow
- **Charts** : Animate on load (stagger 50ms per bar)
- **Notifications badge** : Pulse animation si nouveau
- **Loading states** : Skeleton screens (pas de spinners)

### Gestures (Mobile)
- **Swipe left** sur card → Actions rapides
- **Pull to refresh** sur liste
- **Long press** → Context menu

---

## 📱 Responsive Behavior

### Desktop (>1280px)
- Sidebar 240px + Dashboard + Panel 400px
- Grid 4 colonnes pour KPI cards
- Widgets en 2-3 colonnes

### Tablet (768px - 1280px)
- Sidebar repliable
- Panel lateral devient modal pleine hauteur
- Grid 2 colonnes pour KPI cards
- Widgets stacked ou 2 colonnes

### Mobile (<768px)
- **Top navbar** : Logo + Burger menu + Profil
- **Sidebar** : Drawer overlay depuis la gauche
- **Dashboard** : Single column
- **KPI Cards** : 1 colonne, scroll horizontal ou stack
- **Panel** : Bottom sheet modal
- **Navigation** : Bottom tab bar fixe (5 items principaux)

---

## ⚙️ Fonctionnalités Avancées

### 🎛️ Personnalisation Dashboard
- **Drag & Drop** : Réorganiser widgets (GridStack.js ou react-grid-layout)
- **Resize** : Ajuster taille widgets
- **Hide/Show** : Toggle widgets depuis menu paramètres
- **Presets** : Layouts sauvegardés ("Vue Admin", "Vue Médecin", "Vue Stats")
- **Export layout** : Sauvegarder config JSON

### 🔍 Recherche Intelligente
- **Fuzzy search** : Tolère les typos
- **Shortcuts** :
  - `/p` + texte → Cherche patients
  - `/o` + texte → Cherche ordonnances
  - `/date:today` → Filtre par date
- **Historique** : Dernières recherches
- **Suggestions** : Auto-complete basé sur historique

### 📊 Exports
- **CSV** : Tableaux de données
- **PDF** : Rapports formatés
- **Excel** : Export complexe avec formules
- **Print** : Vue optimisée impression

### 🔔 Notifications Temps Réel
- **WebSocket** ou **Polling** : Updates live
- **Push notifications** : Si PWA activé
- **Sons** : Optionnel pour urgences
- **Do Not Disturb** : Mode focus

---

## 🚀 Stack Technique Recommandée

### Frontend Framework
- **Vanilla JS moderne** (ES6+) : Pour cohérence avec existant
- OU **Vue.js 3** : Léger, progressif, facile à intégrer
- OU **React** : Écosystème riche pour dashboard

### UI Components
- **Headless UI** : Components accessibles
- **Radix UI** : Primitives unstyled
- OU construire custom avec CSS moderne

### Charts
- **Chart.js** : Simple, léger
- **Apache ECharts** : Plus puissant, thèmes pro
- **D3.js** : Max customisation (plus complexe)

### Drag & Drop
- **SortableJS** : Vanilla, léger
- **GridStack.js** : Pour dashboard widgets

### Icons
- **Lucide Icons** : Modern, consistent
- **Heroicons** : Tailwind ecosystem
- **Phosphor Icons** : Grande variété

### Animations
- **GSAP** : Pro animations
- OU **CSS Animations** : Pour simplicité

---

## 🎯 Prochaines Étapes

1. **Validation design** : Confirmer que cette direction vous plaît
2. **Wireframe interactif** : Créer prototype Figma/HTML statique (optionel)
3. **Implémentation progressive** :
   - Phase 1 : Structure + Top Navbar + Sidebar
   - Phase 2 : KPI Cards + Widgets principaux
   - Phase 3 : Panel latéral + Interactions
   - Phase 4 : Responsive + Animations
   - Phase 5 : Fonctionnalités avancées

4. **Migration données** : Adapter depuis structure actuelle
5. **Tests utilisateurs** : Feedback et ajustements

---

## 💡 Notes Importantes

**Avantages de cette approche :**
- ✅ Vision d'ensemble immédiate (dashboard central)
- ✅ Accès rapide aux données clés (KPI cards)
- ✅ Multi-tasking (panel latéral)
- ✅ Évolutif (ajout widgets facilement)
- ✅ Moderne et professionnel

**Défis :**
- ⚠️ Complexité initiale développement
- ⚠️ Performance si beaucoup de widgets (lazy loading nécessaire)
- ⚠️ Courbe apprentissage utilisateurs (formation nécessaire)

**Solutions :**
- 🎓 Tutorial guidé au premier lancement
- 📚 Documentation intégrée (tooltips, help center)
- 🎬 Onboarding interactif
- 💾 Sauvegarder préférences utilisateur

---

**Voulez-vous que je commence l'implémentation ?** 🚀
