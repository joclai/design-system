# 🎨 Design System

> **Preview des composants.** Source de vérité unique. Tout composant référence **exclusivement** les tokens définis ici — aucune valeur codée en dur.

---

## Table des matières

1. [Fondations & conventions](#1-fondations--conventions)
2. [Thématisation (dark / light / densité)](#2-thématisation-dark--light--densité)
3. [Palette de couleurs](#3-palette-de-couleurs)
4. [Dégradés](#4-dégradés)
5. [Système d'élévation](#5-système-délévation)
6. [Typographie](#6-typographie)
7. [Espacements, Layout & Densité](#7-espacements-layout--densité)
8. [Motion & Animations](#8-motion--animations)
9. [Composants — Cartes](#9-composants--cartes)
10. [Composants — Boutons](#10-composants--boutons)
11. [Composants — Tabs & Segmented controls](#11-composants--tabs--segmented-controls)
12. [Composants — Tableaux](#12-composants--tableaux)
13. [Composants — Badges](#13-composants--badges)
14. [Composants — Formulaires & Inputs](#14-composants--formulaires--inputs)
15. [Composants — Toggles, Checkboxes & Radios](#15-composants--toggles-checkboxes--radios)
16. [Composants — Progress & Sliders](#16-composants--progress--sliders)
17. [Composants — Modales & Overlays](#17-composants--modales--overlays)
18. [Composants — Toasts & Notifications](#18-composants--toasts--notifications)
19. [Composants — Tooltips & Popovers](#19-composants--tooltips--popovers)
20. [Composants — Dropdowns & Menus](#20-composants--dropdowns--menus)
21. [Composants — Skeleton Loaders](#21-composants--skeleton-loaders)
22. [Composants — Avatars](#22-composants--avatars)
23. [Composants — Navigation latérale & Breadcrumbs](#23-composants--navigation-latérale--breadcrumbs)
24. [Composants — Steppers & Timeline](#24-composants--steppers--timeline)
25. [Composants — Graphiques (Chart.js)](#25-composants--graphiques-chartjs)
26. [États système — Empty & Error](#26-états-système--empty--error)
27. [Page de connexion (Login)](#27-page-de-connexion-login)
28. [Icônes & Émojis](#28-icônes--émojis)
29. [Breakpoints & Responsive](#29-breakpoints--responsive)
30. [Accessibilité](#30-accessibilité)
31. [Variables CSS complètes](#31-variables-css-complètes)

---

## 1. Fondations & conventions

- **Tokens d'abord.** Les tokens sont les briques atomiques de l'interface. Aucun composant ne contient de valeur en dur.
- **Project-agnostic.** Aucune référence à un projet spécifique ; les exemples utilisent des libellés génériques.
- **Thème & densité par attribut.** Le thème et la densité sont pilotés par des attributs `data-*` sur `<html>` — jamais par des classes dispersées.
- **Conventions de nommage :**
  - Dégradés : `--grad-[couleur1]-[couleur2]` (couleurs dominantes). Dégradés réservés aux fonds de page : préfixe `--grad-bg-`.
  - Échelles : `--elevation-*`, `--ease-*`, `--duration-*`, `--density-*`, `--radius-*`.
  - Compatibilité : `--transition-fast|normal|slow` et `--shadow-card|modal` sont conservés comme **alias** des nouvelles échelles (voir §8 et §5).

```html
<html data-theme="dark" data-density="normal">
```

---

## 2. Thématisation (dark / light / densité)

Le **thème sombre est le défaut**. Le thème clair s'active via `data-theme="light"` ; il ne surcharge que les tokens de **surface, texte, bordure, ombre** et les **couleurs à faible contraste**. La structure des composants et les dégradés ne changent pas.

> `--accent` (#6c5ce7) et `--indigo` (#4d6bfe) conservent leur valeur dans les deux thèmes : ils tiennent le contraste sur fond blanc et garantissent la continuité de l'identité visuelle.

### Bascule (JS de référence)

```js
const root = document.documentElement;

function setTheme(theme)   { root.dataset.theme = theme;   localStorage.setItem('theme', theme); }
function setDensity(level) { root.dataset.density = level; localStorage.setItem('density', level); }

// Init : préférence sauvegardée > préférence système > dark
const saved  = localStorage.getItem('theme');
const system = matchMedia('(prefers-color-scheme: light)').matches ? 'light' : 'dark';
setTheme(saved || system);
setDensity(localStorage.getItem('density') || 'normal');
```

### Règles de contraste

| Usage | Règle |
|-------|-------|
| Texte principal (`--text` sur `--card`) | ≥ 4.5:1 dans les deux thèmes |
| Texte coloré (badges, valeurs) | Variantes assombries en light pour tenir ≥ 4.5:1 sur la surface |
| Dégradés en aplat (barres, boutons) | Décoratifs — pas de texte critique dessus, sauf blanc plein |
| Texte sur dégradé (`background-clip: text`) | Réservé aux valeurs ≥ 1.4rem |

---

## 3. Palette de couleurs

### Neutres & sémantiques

| Rôle | Nom | Token | Hex (dark) |
|------|-----|-------|-----|
| **Fond principal** | Noir profond | `--bg` | `#0f1117` |
| **Fond carte** | Gris foncé | `--card` | `#1a1d2a` |
| **Fond contrôles** | Gris moyen | `--card2` | `#212435` |
| **Bordure** | Gris subtil | `--border` | `#2a2d40` |
| **Texte principal** | Blanc cassé | `--text` | `#e0e2f0` |
| **Texte secondaire** | Gris clair | `--muted` | `#7a7d90` |
| **Texte muet** | Gris très clair | `--placeholder` | `#5a5d70` |
| **Violet** | Accent principal | `--accent` | `#6c5ce7` |
| **Bleu** | Info / Balance | `--blue` | `#5c8dff` |
| **Vert** | Succès | `--green` | `#00d68f` |
| **Orange** | Attention | `--orange` | `#ffa726` |
| **Rouge** | Erreur | `--red` | `#ff5252` |

### Palette étendue

| Rôle | Nom | Token | Hex (dark) |
|------|-----|-------|-----|
| **Rose vif** | Highlight / nouveauté | `--pink` | `#f050a0` |
| **Cyan électrique** | Live / temps réel | `--cyan` | `#00d4ff` |
| **Teal** | Tags neutres / secondaires | `--teal` | `#00b8a0` |
| **Indigo** | Accent sombre | `--indigo` | `#4d6bfe` |
| **Jaune** | Avertissement doux | `--yellow` | `#f5d020` |
| **Lime** | Performance / score élevé | `--lime` | `#82e000` |
| **Violet clair** | Labels / catégories | `--purple` | `#c061f7` |
| **Corail** | Alerte douce | `--coral` | `#ff6b6b` |

### Palette tertiaire (nouvelle)

> Ces couleurs complètent la roue chromatique pour les graphiques riches, les catégories nombreuses et les états spécifiques. Elles ne remplacent jamais une couleur sémantique.

| Rôle | Nom | Token | Hex (dark) |
|------|-----|-------|-----|
| **Rose chaud** | Favori / mention | `--rose` | `#ff5c8a` |
| **Ambre doré** | Récompense / jalon | `--amber` | `#ffc24b` |
| **Bleu ciel** | Info secondaire (plus doux que cyan) | `--sky` | `#38b6ff` |
| **Lavande** | Accent doux / état désactivé coloré | `--lavender` | `#b09cff` |
| **Ardoise** | Série de données neutre / désemphasée | `--slate` | `#8593b0` |
| **Magenta** | Catégorie vive | `--magenta` | `#e0399e` |

### Usage sémantique des couleurs

| Contexte | Couleur |
|----------|---------|
| Balance / crédit disponible | `--blue` |
| Consommation / dépense | `--orange` |
| Statut actif, tendance positive, succès | `--green` |
| Erreur, tendance négative, alerte | `--red` |
| Accent UI, sélection active, primaire | `--accent` |
| Texte désactivé, statut inactif | `--placeholder` |
| Données en direct / flux temps réel | `--cyan` |
| Nouveauté, promotion, mise en avant | `--pink` |
| Catégories secondaires, tags neutres | `--teal` |
| Score de performance élevé | `--lime` |
| Avertissement non bloquant | `--yellow` |
| Alerte douce, erreur non critique | `--coral` |
| Labels de catégories UI | `--purple` |
| Favori, élément mis en avant par l'utilisateur | `--rose` |
| Récompense, jalon atteint, distinction | `--amber` |
| Information complémentaire de second plan | `--sky` |
| Accent doux, surbrillance discrète | `--lavender` |
| Série désemphasée, donnée de référence | `--slate` |
| Catégorie vive supplémentaire | `--magenta` |

### Ordre recommandé pour graphiques multi-séries

Maximise la distinction visuelle quand plusieurs séries cohabitent. Les 10 premières positions restent stables ; les suivantes étendent la liste.

```
1.  --accent    #6c5ce7  Violet
2.  --cyan      #00d4ff  Cyan
3.  --pink      #f050a0  Rose
4.  --green     #00d68f  Vert
5.  --yellow    #f5d020  Jaune
6.  --blue      #5c8dff  Bleu
7.  --coral     #ff6b6b  Corail
8.  --lime      #82e000  Lime
9.  --purple    #c061f7  Violet clair
10. --teal      #00b8a0  Teal
11. --rose      #ff5c8a  Rose chaud
12. --sky       #38b6ff  Bleu ciel
13. --lavender  #b09cff  Lavande
14. --magenta   #e0399e  Magenta
```

> `--amber` et `--slate` sont **exclus de l'ordre de distinction** : l'ambre est réservé aux jalons/récompenses, l'ardoise aux séries volontairement désemphasées.

---

## 4. Dégradés

> **Convention :** `--grad-[couleur1]-[couleur2]`. Les dégradés de fond de page utilisent le préfixe `--grad-bg-`.

### Dégradés UI (tuiles, textes, boutons, badges, courbes)

| Variable | Couleurs | Valeur |
|----------|----------|--------|
| `--grad-indigo-violet` | Indigo → Violet | `linear-gradient(90deg, #4d6bfe, #6c5ce7)` |
| `--grad-orange-red` | Orange → Rouge | `linear-gradient(90deg, #ffa726, #ff7043)` |
| `--grad-blue-sky` | Bleu → Bleu ciel | `linear-gradient(90deg, #5c8dff, #42a5f5)` |
| `--grad-green` | Vert → Vert vif | `linear-gradient(90deg, #00d68f, #00e676)` |
| `--grad-pink-purple` | Rose → Violet clair | `linear-gradient(90deg, #f050a0, #c061f7)` |
| `--grad-cyan-teal` | Cyan → Teal | `linear-gradient(90deg, #00d4ff, #00b8a0)` |
| `--grad-lime-green` | Lime → Vert | `linear-gradient(90deg, #82e000, #00d68f)` |
| `--grad-purple-violet` | Violet clair → Indigo | `linear-gradient(90deg, #e040fb, #7c4dff)` |
| `--grad-coral-orange` | Corail → Orange | `linear-gradient(90deg, #ff6b6b, #ffa726)` |
| `--grad-yellow-orange` | Jaune → Orange doux | `linear-gradient(90deg, #feca57, #ff9f43)` |
| `--grad-violet-blue` | Violet → Bleu | `linear-gradient(135deg, #6c5ce7, #5c8dff)` |
| `--grad-rose-amber` | Rose chaud → Ambre | `linear-gradient(90deg, #ff5c8a, #ffc24b)` |
| `--grad-sky-lavender` | Bleu ciel → Lavande | `linear-gradient(90deg, #38b6ff, #b09cff)` |
| `--grad-magenta-rose` | Magenta → Rose chaud | `linear-gradient(90deg, #e0399e, #ff5c8a)` |
| `--grad-login-bar` | Violet → Vert → Bleu | `linear-gradient(90deg, #6c5ce7, #00d68f, #5c8dff)` |

### Dégradés de fond (`--grad-bg-*`)

| Variable | Description | Valeur |
|----------|-------------|--------|
| `--grad-bg-login` | Fond pleine page login | `linear-gradient(135deg, #0f1117, #1a1d2a, #0f1117)` |

### Matrice d'usages courants

Tous les dégradés UI sont utilisables sur l'ensemble des supports suivants :

| Support | Barre top tuile | Texte tuile | Courbe chart | Bouton | Badge |
|---------|:-:|:-:|:-:|:-:|:-:|
| Compatibilité | ✅ | ✅ | ✅ | ✅ | ✅ |

---

## 5. Système d'élévation

Cinq niveaux d'ombre tokenisés. `--shadow-card` et `--shadow-modal` sont conservés comme **alias** des niveaux 2 et 4.

```css
:root {
  --elevation-0: none;                              /* À plat — éléments intégrés au fond */
  --elevation-1: 0 1px 3px rgba(0, 0, 0, 0.25);     /* Léger relief — chips, avatars */
  --elevation-2: 0 4px 24px rgba(0, 0, 0, 0.30);    /* Cartes, sections (= --shadow-card) */
  --elevation-3: 0 12px 40px rgba(0, 0, 0, 0.40);   /* Dropdowns, popovers, toasts */
  --elevation-4: 0 25px 80px rgba(0, 0, 0, 0.50);   /* Modales (= --shadow-modal) */
}

html[data-theme="light"] {
  --elevation-1: 0 1px 3px rgba(20, 24, 50, 0.08);
  --elevation-2: 0 4px 24px rgba(20, 24, 50, 0.08);
  --elevation-3: 0 12px 40px rgba(20, 24, 50, 0.12);
  --elevation-4: 0 25px 80px rgba(20, 24, 50, 0.18);
}
```

### Matrice d'attribution

| Niveau | Token | Composants |
|--------|-------|------------|
| 0 | `--elevation-0` | Tableaux, inputs au repos, badges, sidebar |
| 1 | `--elevation-1` | Chips actifs, segment actif, avatars |
| 2 | `--elevation-2` | Cartes, tuiles stat, sections de graphique |
| 3 | `--elevation-3` | Dropdowns, popovers, tooltips riches, toasts |
| 4 | `--elevation-4` | Modales, panneaux latéraux superposés |

> **Règle :** un élément ne saute jamais plus d'un niveau lors d'une interaction (ex. carte au hover : 2 → 3 maximum).

---

## 6. Typographie

### Familles de polices

```css
--font-ui:    -apple-system, BlinkMacSystemFont, 'Segoe UI', system-ui, sans-serif;
--font-login: 'Inter', -apple-system, system-ui, sans-serif;   /* charge depuis Google Fonts */
--font-mono:  'SF Mono', 'Fira Code', 'Cascadia Code', monospace;
```

### Échelle typographique

| Élément | Taille | Poids | Style / Notes |
|---------|--------|-------|---------------|
| **Titre principal (h1)** | `1.6rem` | `700` | Dégradé violet→bleu |
| **Titre de section (h2)** | `1rem` | `600` | Couleur `--text` |
| **Titre de graphique** | `0.85rem` | `500` | Couleur `--muted` |
| **Label de carte** | `0.75rem` | `500` | Uppercase, `letter-spacing: 0.08em`, `--muted` |
| **Valeur principale de carte** | `1.8rem` | `700` | Dégradé selon catégorie |
| **Sous-valeur / tendance** | `0.8rem` | `400` | `--muted` |
| **Corps de tableau** | `0.85rem` | `400` | `--text` |
| **En-tête tableau** | `0.85rem` | `500` | `--muted` |
| **Boutons** | `0.85rem` | `500` | — |
| **Badges** | `0.75rem` | `500` | — |
| **Monospace** | `0.8rem` | `400` | Valeurs techniques |

---

## 7. Espacements, Layout & Densité

### Système d'espacement (base 4px)

```
4px  — micro (entre badge et texte)
8px  — XS (padding boutons compacts)
12px — SM (padding mobile, gap interne)
16px — MD (gap de grille cartes)
20px — LG (padding carte, padding page)
24px — XL (margin entre sections)
30px — 2XL (margin header)
48px — 3XL (padding carte login)
```

### Densité d'affichage

Trois modes pilotés par `data-density`. Seuls les **espacements internes** varient — jamais les tailles de police ni les rayons. Cible les surfaces de **données répétitives** (tableaux, inputs, menus, sidebar), pas les surfaces de lecture (cartes, modales, toasts conservent un padding fixe).

```css
:root,
html[data-density="normal"]      { --density-pad-y: 10px; --density-pad-x: 14px; --density-gap: 12px; }
html[data-density="compact"]     { --density-pad-y: 6px;  --density-pad-x: 10px; --density-gap: 8px;  }
html[data-density="comfortable"] { --density-pad-y: 14px; --density-pad-x: 18px; --density-gap: 16px; }
```

### Layout général

```css
body      { padding: 20px; background: var(--bg); }   /* 12px sur mobile */
.container { max-width: 1200px; margin: 0 auto; }

.cards-grid  { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 16px; }
.charts-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
```

---

## 8. Motion & Animations

### Courbes d'easing nommées

```css
:root {
  --ease-standard: ease;                                /* Transitions simples */
  --ease-out-expo: cubic-bezier(0.16, 1, 0.3, 1);       /* Entrées (modales, toasts) */
  --ease-in-out:   cubic-bezier(0.65, 0, 0.35, 1);      /* Déplacements, layout */
  --ease-spring:   cubic-bezier(0.34, 1.56, 0.64, 1);   /* Micro-interactions (switch, checkbox) */
}
```

### Durées par catégorie d'interaction

`--transition-fast|normal|slow` sont conservés comme alias de `--duration-fast|normal|slow`.

```css
:root {
  --duration-instant: 0.1s;   /* Pressed state */
  --duration-fast:    0.15s;  /* Hover, focus (= --transition-fast) */
  --duration-normal:  0.2s;   /* État de composant (= --transition-normal) */
  --duration-slow:    0.3s;   /* Layout, accordéons (= --transition-slow) */
  --duration-overlay: 0.25s;  /* Apparition modale / backdrop */
  --duration-toast:   0.35s;  /* Entrée / sortie de toast */
}
```

| Interaction | Durée | Easing |
|-------------|-------|--------|
| Pressed (boutons, segments) | `--duration-instant` | `--ease-standard` |
| Hover / focus | `--duration-fast` | `--ease-standard` |
| Switch, checkbox, radio | `--duration-normal` | `--ease-spring` |
| Ouverture dropdown / popover | `--duration-normal` | `--ease-out-expo` |
| Ouverture modale | `--duration-overlay` | `--ease-out-expo` |
| Entrée / sortie toast | `--duration-toast` | `--ease-out-expo` |
| Accordéon, changement de hauteur | `--duration-slow` | `--ease-in-out` |
| Barre de progression | `--duration-slow` | `--ease-in-out` |

### Animations de référence

```css
/* Pressed universel */
.btn:active, .filter-btn:active, .pag-page:active {
  transform: scale(0.97);
  transition-duration: var(--duration-instant);
}

/* Loader */
.loader {
  width: 20px; height: 20px;
  border: 2px solid var(--border);
  border-top-color: var(--accent);
  border-radius: 50%;
  animation: spin 0.7s linear infinite;
}
@keyframes spin { to { transform: rotate(360deg); } }

/* Apparition de carte (page load) */
.card { animation: fadeUp 0.3s ease both; }
.card:nth-child(1) { animation-delay: 0.05s; }
.card:nth-child(2) { animation-delay: 0.10s; }
.card:nth-child(3) { animation-delay: 0.15s; }
.card:nth-child(4) { animation-delay: 0.20s; }
@keyframes fadeUp { from { opacity: 0; transform: translateY(12px); } to { opacity: 1; transform: translateY(0); } }

/* Pulse (statut actif) */
.status-pulse {
  display: inline-block; width: 8px; height: 8px;
  border-radius: 50%; background: var(--green);
  animation: pulse 2s ease infinite;
}
@keyframes pulse { 0%, 100% { opacity: 1; transform: scale(1); } 50% { opacity: 0.5; transform: scale(0.85); } }
```

> **Réduction de mouvement :** la media query `prefers-reduced-motion: reduce` (voir §30) s'applique à **toutes** les animations sans exception.

---

## 9. Composants — Cartes

```css
.card {
  background: var(--card);
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);
  padding: 20px;
  position: relative;
  overflow: hidden;
  box-shadow: var(--elevation-2);
  transition: border-color var(--transition-normal);
}
.card:hover { border-color: rgba(108, 92, 231, 0.35); }

/* Barre colorée en haut — à spécialiser */
.card::before { content: ''; position: absolute; top: 0; left: 0; right: 0; height: 3px; }
```

### Spécialisations par type

```css
.card.balance::before     { background: var(--grad-indigo-violet); }
.card.consumption::before { background: var(--grad-orange-red); }
.card.snapshots::before   { background: var(--grad-blue-sky); }
.card.api-status::before  { background: var(--grad-green); }
.card.rhythm::before      { background: var(--grad-purple-violet); }
.card.live::before        { background: var(--grad-cyan-teal); }
.card.highlight::before   { background: var(--grad-pink-purple); }
.card.performance::before { background: var(--grad-lime-green); }
.card.alert-soft::before  { background: var(--grad-coral-orange); }
.card.favorite::before    { background: var(--grad-rose-amber); }
.card.secondary::before   { background: var(--grad-sky-lavender); }
```

### Contenu interne

```css
.card-label {
  font-size: 0.75rem; text-transform: uppercase;
  letter-spacing: 0.08em; color: var(--muted); margin-bottom: 6px;
}
.card-value { font-size: 1.8rem; font-weight: 700; line-height: 1.2; }
.card-sub   { font-size: 0.8rem; color: var(--muted); margin-top: 4px; }

/* Valeur en dégradé (texte) */
.card-value.accent { background: var(--grad-indigo-violet); -webkit-background-clip: text; background-clip: text; color: transparent; }
.card-value.orange { background: var(--grad-orange-red);    -webkit-background-clip: text; background-clip: text; color: transparent; }
.card-value.blue   { background: var(--grad-blue-sky);      -webkit-background-clip: text; background-clip: text; color: transparent; }
.card-value.green  { background: var(--grad-green);         -webkit-background-clip: text; background-clip: text; color: transparent; }
.card-value.pink   { background: var(--grad-pink-purple);   -webkit-background-clip: text; background-clip: text; color: transparent; }
.card-value.rose   { background: var(--grad-rose-amber);    -webkit-background-clip: text; background-clip: text; color: transparent; }
```

### Tuiles statistiques (variante compacte, barre 2px)

```css
.stat-tile {
  position: relative; overflow: hidden;
  background: var(--card); border: 1px solid var(--border);
  border-radius: var(--radius-lg); padding: 16px 20px;
}
.stat-tile::before { content: ''; position: absolute; top: 0; left: 0; right: 0; height: 2px; }
.stat-tile:nth-child(1)::before { background: var(--grad-coral-orange); }
.stat-tile:nth-child(2)::before { background: var(--grad-cyan-teal); }
.stat-tile:nth-child(3)::before { background: var(--grad-yellow-orange); }
.stat-tile:nth-child(4)::before { background: var(--grad-indigo-violet); }
```

---

## 10. Composants — Boutons

> **⚠️ Règle tactile :** tous les `:hover` des boutons interactifs sont protégés par `@media (hover: hover)` pour éviter le "stuck hover" sur écran tactile.

```css
/* Secondaire (header, contrôles) */
.btn {
  background: var(--card2); color: var(--text);
  border: 1px solid var(--border);
  padding: 8px 16px; border-radius: var(--radius-md);
  cursor: pointer; font-size: 0.85rem; font-family: var(--font-ui);
  transition: all var(--transition-normal); white-space: nowrap;
}
@media (hover: hover) { .btn:hover { background: var(--grad-violet-blue); border-color: var(--accent); color: #fff; } }
.btn:active   { transform: scale(0.97); transition-duration: var(--duration-instant); }
.btn:disabled { opacity: 0.5; cursor: not-allowed; }

/* Primaire (login, actions principales) */
.btn-primary {
  width: 100%; padding: 12px 20px;
  background: var(--grad-violet-blue); border: none; border-radius: 10px;
  color: #fff; font-size: 1rem; font-weight: 600; cursor: pointer;
  transition: all var(--transition-normal);
}
.btn-primary:hover  { background: #7c6cf0; transform: translateY(-1px); box-shadow: 0 8px 24px rgba(108, 92, 231, 0.4); }
.btn-primary:active { transform: scale(0.97); }

/* Filtres (1h / 1j / 7j / 30j) */
.filter-btn {
  padding: 4px 10px; background: var(--card2);
  border: 1px solid var(--border); border-radius: var(--radius-sm);
  color: var(--muted); font-size: 0.75rem; cursor: pointer;
  transition: all var(--transition-fast);
}
@media (hover: hover) { .filter-btn:hover { background: var(--grad-violet-blue); border-color: var(--accent); color: #fff; } }
.filter-btn.active { background: var(--grad-violet-blue); border-color: var(--accent); color: #fff; }
```

> Boutons de pagination (`.pag-page`, `.nav-btn`, `.pag-btn`) et de scroll (`.scroll-btn`) suivent le même motif : fond `--card2`, hover/active en `--grad-violet-blue`, hover protégé par `@media (hover: hover)`.

---

## 11. Composants — Tabs & Segmented controls

```css
/* Tabs — sections de contenu distinctes */
.tabs { display: flex; gap: 4px; border-bottom: 1px solid var(--border); }
.tab {
  background: none; border: none; border-bottom: 2px solid transparent;
  color: var(--muted); font-size: 0.85rem; font-family: var(--font-ui);
  padding: 10px 16px; margin-bottom: -1px; cursor: pointer;
  transition: all var(--transition-fast);
}
@media (hover: hover) { .tab:hover { color: var(--text); } }
.tab.active { color: var(--accent); border-bottom-color: var(--accent); font-weight: 500; }

/* Segmented — vues alternatives du même contenu */
.segmented {
  display: inline-flex; background: var(--card2);
  border: 1px solid var(--border); border-radius: var(--radius-md);
  padding: 3px; gap: 2px;
}
.segment {
  background: none; border: none; border-radius: var(--radius-sm);
  color: var(--muted); font-size: 0.78rem; font-family: var(--font-ui);
  padding: 5px 14px; cursor: pointer; transition: all var(--transition-fast);
}
.segment.active { background: var(--card); color: var(--text); box-shadow: var(--elevation-1); font-weight: 500; }
```

| Composant | Usage |
|-----------|-------|
| Tabs | Sections distinctes (détail, historique, paramètres) |
| Segmented | Vues alternatives du **même** contenu (liste / grille) |
| Filter buttons | Filtres temporels de graphiques (1h / 1j / 7j / 30j) |

---

## 12. Composants — Tableaux

```css
.table-wrap {
  background: var(--card); border: 1px solid var(--border);
  border-radius: var(--radius-lg); overflow-x: auto; margin-bottom: 24px;
}
table { width: 100%; border-collapse: collapse; font-size: 0.85rem; }
th {
  text-align: left; padding: var(--density-pad-y) var(--density-pad-x);
  color: var(--muted); font-weight: 500; border-bottom: 1px solid var(--border); white-space: nowrap;
}
td {
  padding: var(--density-pad-y) var(--density-pad-x);
  border-bottom: 1px solid var(--border); color: var(--text); vertical-align: middle;
}
tr:last-child td { border: none; }
@media (hover: hover) { tbody tr:hover td { background: rgba(108, 92, 231, 0.05); } }
td.mono { font-family: var(--font-mono); font-size: 0.8rem; color: var(--muted); }
```

> Le padding des cellules est piloté par la densité (§7).

---

## 13. Composants — Badges

```css
.badge {
  display: inline-flex; align-items: center; gap: 4px;
  padding: 2px 8px; border-radius: 4px;
  font-size: 0.75rem; font-weight: 500; line-height: 1.6;
}

/* Sémantiques */
.badge.green  { background: rgba(0, 214, 143, 0.15);  color: var(--green); }
.badge.red    { background: rgba(255, 82, 82, 0.15);   color: var(--red); }
.badge.orange { background: rgba(255, 167, 38, 0.15);  color: var(--orange); }
.badge.blue   { background: rgba(92, 141, 255, 0.15);  color: var(--blue); }
.badge.accent { background: rgba(108, 92, 231, 0.15);  color: var(--accent); }
.badge.muted  { background: rgba(122, 125, 144, 0.15); color: var(--muted); }

/* Étendues */
.badge.pink   { background: rgba(240, 80, 160, 0.15);  color: var(--pink); }
.badge.cyan   { background: rgba(0, 212, 255, 0.15);   color: var(--cyan); }
.badge.teal   { background: rgba(0, 184, 160, 0.15);   color: var(--teal); }
.badge.indigo { background: rgba(77, 107, 254, 0.15);  color: var(--indigo); }
.badge.yellow { background: rgba(245, 208, 32, 0.15);  color: var(--yellow); }
.badge.lime   { background: rgba(130, 224, 0, 0.15);   color: var(--lime); }
.badge.purple { background: rgba(192, 97, 247, 0.15);  color: var(--purple); }
.badge.coral  { background: rgba(255, 107, 107, 0.15); color: var(--coral); }

/* Tertiaires */
.badge.rose     { background: rgba(255, 92, 138, 0.15);  color: var(--rose); }
.badge.amber    { background: rgba(255, 194, 75, 0.15);  color: var(--amber); }
.badge.sky      { background: rgba(56, 182, 255, 0.15);  color: var(--sky); }
.badge.lavender { background: rgba(176, 156, 255, 0.15); color: var(--lavender); }
.badge.slate    { background: rgba(133, 147, 176, 0.15); color: var(--slate); }
.badge.magenta  { background: rgba(224, 57, 158, 0.15);  color: var(--magenta); }
```

---

## 14. Composants — Formulaires & Inputs

```css
.input-group { display: flex; flex-direction: column; gap: 6px; margin-bottom: 16px; }
.input-label { font-size: 0.8rem; font-weight: 500; color: var(--muted); letter-spacing: 0.03em; }

.input {
  background: rgba(15, 17, 23, 0.6);
  border: 1px solid var(--border); border-radius: 10px;
  padding: var(--density-pad-y) var(--density-pad-x);
  color: var(--text); font-size: 0.9rem; font-family: var(--font-ui);
  transition: border-color var(--transition-normal), box-shadow var(--transition-normal);
  outline: none; width: 100%; box-sizing: border-box;
}
.input::placeholder { color: var(--placeholder); }
.input:focus    { border-color: var(--accent); box-shadow: 0 0 0 3px rgba(108, 92, 231, 0.2); }
.input:disabled { opacity: 0.5; cursor: not-allowed; }
.input.invalid  { border-color: var(--red); box-shadow: 0 0 0 3px rgba(255, 82, 82, 0.15); }

/* Select */
select.input {
  cursor: pointer; appearance: none;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='12' viewBox='0 0 12 12'%3E%3Cpath fill='%237a7d90' d='M6 8L1 3h10z'/%3E%3C/svg%3E");
  background-repeat: no-repeat; background-position: right 12px center; padding-right: 32px;
}

/* Erreur sous champ */
.field-error { font-size: 0.75rem; color: var(--red); margin-top: 4px; display: flex; align-items: center; gap: 5px; }
```

---

## 15. Composants — Toggles, Checkboxes & Radios

```css
/* Switch */
.switch { position: relative; width: 38px; height: 22px; flex-shrink: 0; display: inline-block; }
.switch input { opacity: 0; width: 0; height: 0; }
.switch-track {
  position: absolute; inset: 0; background: var(--card2); border: 1px solid var(--border);
  border-radius: 999px; cursor: pointer; transition: all var(--duration-normal) var(--ease-spring);
}
.switch-track::before {
  content: ''; position: absolute; top: 2px; left: 2px; width: 16px; height: 16px;
  background: var(--muted); border-radius: 50%; transition: all var(--duration-normal) var(--ease-spring);
}
.switch input:checked + .switch-track { background: var(--grad-violet-blue); border-color: var(--accent); }
.switch input:checked + .switch-track::before { transform: translateX(16px); background: #fff; }
.switch input:focus-visible + .switch-track { outline: 2px solid var(--accent); outline-offset: 2px; }

/* Checkbox */
.checkbox { display: inline-flex; align-items: center; gap: 9px; cursor: pointer; font-size: 0.85rem; }
.checkbox input { opacity: 0; width: 0; height: 0; position: absolute; }
.checkbox-box {
  width: 17px; height: 17px; border: 1.5px solid var(--border); border-radius: 4px;
  background: var(--card2); display: inline-flex; align-items: center; justify-content: center;
  transition: all var(--duration-normal) var(--ease-spring); flex-shrink: 0;
}
.checkbox-box::after { content: '✓'; color: #fff; font-size: 0.65rem; transform: scale(0); transition: transform var(--duration-normal) var(--ease-spring); }
.checkbox input:checked + .checkbox-box { background: var(--accent); border-color: var(--accent); }
.checkbox input:checked + .checkbox-box::after { transform: scale(1); }
.checkbox input:focus-visible + .checkbox-box { outline: 2px solid var(--accent); outline-offset: 2px; }

/* Radio */
.radio { display: inline-flex; align-items: center; gap: 9px; cursor: pointer; font-size: 0.85rem; }
.radio input { opacity: 0; width: 0; height: 0; position: absolute; }
.radio-dot {
  width: 17px; height: 17px; border: 1.5px solid var(--border); border-radius: 50%;
  background: var(--card2); display: inline-flex; align-items: center; justify-content: center;
  transition: all var(--duration-normal) var(--ease-spring); flex-shrink: 0;
}
.radio-dot::after { content: ''; width: 7px; height: 7px; border-radius: 50%; background: var(--accent); transform: scale(0); transition: transform var(--duration-normal) var(--ease-spring); }
.radio input:checked + .radio-dot { border-color: var(--accent); }
.radio input:checked + .radio-dot::after { transform: scale(1); }
.radio input:focus-visible + .radio-dot { outline: 2px solid var(--accent); outline-offset: 2px; }
```

---

## 16. Composants — Progress & Sliders

```css
.progress { height: 6px; background: var(--card2); border-radius: 999px; overflow: hidden; }
.progress-bar { height: 100%; background: var(--grad-violet-blue); border-radius: 999px; transition: width var(--duration-slow) var(--ease-in-out); }
.progress-bar.green  { background: var(--grad-green); }
.progress-bar.orange { background: var(--grad-orange-red); }
.progress-bar.cyan   { background: var(--grad-cyan-teal); }

/* Indéterminée */
.progress.indeterminate .progress-bar { width: 35%; animation: indeterminate 1.2s var(--ease-in-out) infinite; }
@keyframes indeterminate { from { transform: translateX(-110%); } to { transform: translateX(390%); } }

/* Slider (input range) */
.slider { appearance: none; -webkit-appearance: none; width: 100%; height: 6px; background: var(--card2); border-radius: 999px; outline: none; cursor: pointer; }
.slider::-webkit-slider-thumb {
  appearance: none; -webkit-appearance: none; width: 16px; height: 16px; border-radius: 50%;
  background: var(--accent); border: 2px solid var(--card); box-shadow: var(--elevation-1);
  transition: transform var(--duration-fast) var(--ease-standard);
}
.slider::-webkit-slider-thumb:hover { transform: scale(1.15); }
.slider::-moz-range-thumb { width: 16px; height: 16px; border-radius: 50%; background: var(--accent); border: 2px solid var(--card); }
.slider:focus-visible { outline: 2px solid var(--accent); outline-offset: 4px; }
```

---

## 17. Composants — Modales & Overlays

```html
<div class="modal-backdrop" hidden>
  <div class="modal" role="dialog" aria-modal="true" aria-labelledby="modal-title">
    <div class="modal-header">
      <h3 id="modal-title">Titre</h3>
      <button class="modal-close" aria-label="Fermer">✕</button>
    </div>
    <div class="modal-body"><!-- Contenu --></div>
    <div class="modal-footer">
      <button class="btn">Annuler</button>
      <button class="btn-primary">Confirmer</button>
    </div>
  </div>
</div>
```

```css
.modal-backdrop {
  position: fixed; inset: 0; background: rgba(8, 9, 14, 0.65);
  backdrop-filter: blur(4px); -webkit-backdrop-filter: blur(4px);
  display: flex; align-items: center; justify-content: center; padding: 20px; z-index: 100;
  animation: backdropIn var(--duration-overlay) var(--ease-out-expo) both;
}
html[data-theme="light"] .modal-backdrop { background: rgba(28, 30, 43, 0.4); }

.modal {
  background: var(--card); border: 1px solid var(--border);
  border-radius: var(--radius-xl); box-shadow: var(--elevation-4);
  width: 480px; max-width: 100%; max-height: 85vh;
  display: flex; flex-direction: column; overflow: hidden; position: relative;
  animation: modalIn var(--duration-overlay) var(--ease-out-expo) both;
}
.modal::before { content: ''; position: absolute; top: 0; left: 0; right: 0; height: 3px; background: var(--grad-indigo-violet); }
.modal.modal-danger::before { background: var(--grad-coral-orange); }

.modal-header { display: flex; align-items: center; justify-content: space-between; padding: 20px 24px 0; }
.modal-header h3 { font-size: 1.05rem; font-weight: 600; }
.modal-close { background: none; border: none; color: var(--muted); font-size: 0.9rem; cursor: pointer; padding: 6px; border-radius: var(--radius-sm); transition: all var(--transition-fast); }
@media (hover: hover) { .modal-close:hover { background: var(--card2); color: var(--text); } }
.modal-body   { padding: 16px 24px; overflow-y: auto; font-size: 0.88rem; color: var(--muted); line-height: 1.6; }
.modal-footer { display: flex; justify-content: flex-end; gap: 10px; padding: 0 24px 20px; }

@keyframes backdropIn { from { opacity: 0; } to { opacity: 1; } }
@keyframes modalIn { from { opacity: 0; transform: translateY(16px) scale(0.97); } to { opacity: 1; transform: translateY(0) scale(1); } }
```

| Variante | Largeur | Usage |
|----------|---------|-------|
| `.modal` | 480px | Confirmation, formulaire court |
| `.modal.modal-lg` | 720px | Formulaire complet, détail |
| `.modal.modal-danger` | — | Barre `--grad-coral-orange` pour actions destructives |

**Interaction :** clic sur le backdrop = fermeture (sauf saisie non sauvegardée) ; `Échap` ferme toujours ; focus piégé puis restitué au déclencheur.

---

## 18. Composants — Toasts & Notifications

```css
.toast-container { position: fixed; bottom: 20px; right: 20px; display: flex; flex-direction: column; gap: 10px; z-index: 110; max-width: 380px; }
.toast {
  display: flex; align-items: flex-start; gap: 10px;
  background: var(--card); border: 1px solid var(--border); border-left: 3px solid var(--accent);
  border-radius: var(--radius-md); box-shadow: var(--elevation-3); padding: 12px 14px; font-size: 0.85rem;
  animation: toastIn var(--duration-toast) var(--ease-out-expo) both;
}
.toast.leaving { animation: toastOut var(--duration-toast) var(--ease-in-out) both; }
.toast.success { border-left-color: var(--green); }
.toast.error   { border-left-color: var(--red); }
.toast.warning { border-left-color: var(--orange); }
.toast.info    { border-left-color: var(--blue); }
.toast-icon  { flex-shrink: 0; line-height: 1.4; }
.toast-title { font-weight: 600; color: var(--text); margin-bottom: 2px; }
.toast-text  { color: var(--muted); font-size: 0.8rem; line-height: 1.5; }

@keyframes toastIn  { from { opacity: 0; transform: translateX(24px); } to { opacity: 1; transform: translateX(0); } }
@keyframes toastOut { from { opacity: 1; transform: translateX(0); }  to { opacity: 0; transform: translateX(24px); } }
```

| Variante | Icône | Durée | Fermeture manuelle |
|----------|-------|-------|--------------------|
| `success` | ✓ | 4s | Optionnelle |
| `info` | ℹ | 5s | Optionnelle |
| `warning` | ⚠ | 7s | Recommandée |
| `error` | ✕ | Persistant | **Obligatoire** |

Maximum **3 toasts** simultanés (le plus ancien évincé). Bas-droite sur desktop, pleine largeur en bas sur mobile. Conteneur en `aria-live="polite"` (`assertive` réservé aux erreurs bloquantes).

---

## 19. Composants — Tooltips & Popovers

```css
/* Tooltip — texte court, hover/focus */
.tooltip-trigger { position: relative; }
.tooltip {
  position: absolute; bottom: calc(100% + 8px); left: 50%; transform: translateX(-50%);
  background: var(--card2); border: 1px solid var(--border); border-radius: var(--radius-sm);
  box-shadow: var(--elevation-3); color: var(--text); font-size: 0.72rem; padding: 5px 9px;
  white-space: nowrap; pointer-events: none; opacity: 0;
  transition: opacity var(--duration-fast) var(--ease-standard); z-index: 50;
}
.tooltip-trigger:hover .tooltip, .tooltip-trigger:focus-visible .tooltip { opacity: 1; }

/* Popover — contenu riche, au clic */
.popover {
  position: absolute; top: calc(100% + 8px);
  background: var(--card); border: 1px solid var(--border); border-radius: var(--radius-lg);
  box-shadow: var(--elevation-3); padding: 14px 16px; width: 260px; z-index: 60;
  animation: popIn var(--duration-normal) var(--ease-out-expo) both;
}
.popover-title { font-size: 0.82rem; font-weight: 600; margin-bottom: 6px; }
.popover-text  { font-size: 0.78rem; color: var(--muted); line-height: 1.55; }
@keyframes popIn { from { opacity: 0; transform: translateY(-6px); } to { opacity: 1; transform: translateY(0); } }
```

Tooltip : jamais d'information indispensable (inaccessible au tactile), délai ~300ms. Popover : fermeture au clic extérieur et à `Échap`, un seul ouvert à la fois.

---

## 20. Composants — Dropdowns & Menus

```css
.dropdown { position: relative; display: inline-block; }
.dropdown-menu {
  position: absolute; top: calc(100% + 6px); left: 0; min-width: 200px;
  background: var(--card); border: 1px solid var(--border); border-radius: var(--radius-md);
  box-shadow: var(--elevation-3); padding: 5px; z-index: 60;
  animation: popIn var(--duration-normal) var(--ease-out-expo) both;
}
.dropdown-item {
  display: flex; align-items: center; gap: 8px; width: 100%;
  background: none; border: none; border-radius: var(--radius-sm); color: var(--text);
  font-size: 0.82rem; font-family: var(--font-ui);
  padding: var(--density-pad-y) var(--density-pad-x);
  cursor: pointer; text-align: left; transition: background var(--transition-fast);
}
@media (hover: hover) { .dropdown-item:hover { background: rgba(108, 92, 231, 0.1); } }
.dropdown-item.danger { color: var(--red); }
.dropdown-divider { height: 1px; background: var(--border); margin: 5px 0; }
```

Navigation clavier complète (`↑`/`↓`, `Entrée`, `Échap`). Items destructifs (`.danger`) en dernier, séparés par un `.dropdown-divider`.

---

## 21. Composants — Skeleton Loaders

```css
.skeleton { position: relative; overflow: hidden; background: var(--card2); border-radius: var(--radius-sm); }
.skeleton::after {
  content: ''; position: absolute; inset: 0; transform: translateX(-100%);
  background: linear-gradient(90deg, transparent, rgba(224, 226, 240, 0.06), transparent);
  animation: shimmer 1.4s var(--ease-in-out) infinite;
}
html[data-theme="light"] .skeleton::after { background: linear-gradient(90deg, transparent, rgba(28, 30, 43, 0.05), transparent); }
@keyframes shimmer { to { transform: translateX(100%); } }

.skeleton.text   { height: 12px; width: 100%; }
.skeleton.title  { height: 18px; width: 60%; }
.skeleton.value  { height: 28px; width: 40%; }
.skeleton.avatar { width: 36px; height: 36px; border-radius: 50%; }
.skeleton.chart  { height: 180px; border-radius: var(--radius-md); }
```

Reproduit la **silhouette** du contenu final (mêmes dimensions) pour éviter tout layout shift. Affiché au premier rendu si la donnée manque, jamais après un contenu déjà affiché. Au-delà de 8s, basculer vers un état d'erreur.

---

## 22. Composants — Avatars

```css
.avatar {
  width: 36px; height: 36px; border-radius: 50%;
  background: var(--grad-violet-blue); color: #fff;
  display: inline-flex; align-items: center; justify-content: center;
  font-size: 0.78rem; font-weight: 600; flex-shrink: 0;
  border: 2px solid var(--card); box-shadow: var(--elevation-1);
}
.avatar.sm { width: 26px; height: 26px; font-size: 0.62rem; }
.avatar.lg { width: 48px; height: 48px; font-size: 0.95rem; }

/* Rotation de fonds — initiales sans image */
.avatar.g1 { background: var(--grad-violet-blue); }
.avatar.g2 { background: var(--grad-cyan-teal); }
.avatar.g3 { background: var(--grad-pink-purple); }
.avatar.g4 { background: var(--grad-coral-orange); }
.avatar.g5 { background: var(--grad-lime-green); }
.avatar.g6 { background: var(--grad-sky-lavender); }
.avatar.g7 { background: var(--grad-rose-amber); }

/* Groupe empilé */
.avatar-group { display: inline-flex; }
.avatar-group .avatar:not(:first-child) { margin-left: -10px; }
.avatar-group .avatar.more { background: var(--card2); color: var(--muted); font-size: 0.68rem; }

/* Présence */
.avatar-wrap { position: relative; display: inline-block; }
.avatar-status { position: absolute; bottom: 0; right: 0; width: 10px; height: 10px; border-radius: 50%; border: 2px solid var(--card); background: var(--green); }
.avatar-status.away    { background: var(--orange); }
.avatar-status.offline { background: var(--placeholder); }
```

> L'attribution `g1`–`g7` se fait par hash stable de l'identifiant (ex. `id % 7`) — jamais aléatoirement.

---

## 23. Composants — Navigation latérale & Breadcrumbs

```css
.sidebar { width: 220px; background: var(--card); border-right: 1px solid var(--border); padding: 16px 10px; display: flex; flex-direction: column; gap: 2px; }
.sidebar-section { font-size: 0.65rem; text-transform: uppercase; letter-spacing: 0.1em; color: var(--placeholder); padding: 14px 12px 6px; }
.sidebar-item {
  display: flex; align-items: center; gap: 10px;
  padding: var(--density-pad-y) 12px; border-radius: var(--radius-md);
  color: var(--muted); font-size: 0.85rem; cursor: pointer;
  border: none; background: none; font-family: var(--font-ui); width: 100%; text-align: left;
  transition: all var(--transition-fast); position: relative;
}
@media (hover: hover) { .sidebar-item:hover { background: var(--card2); color: var(--text); } }
.sidebar-item.active { background: rgba(108, 92, 231, 0.12); color: var(--accent); font-weight: 500; }
.sidebar-item.active::before { content: ''; position: absolute; left: 0; top: 20%; bottom: 20%; width: 3px; border-radius: 999px; background: var(--grad-indigo-violet); }
.sidebar-badge { margin-left: auto; }

/* Breadcrumbs */
.breadcrumbs { display: flex; align-items: center; gap: 8px; font-size: 0.8rem; }
.breadcrumb-item { color: var(--muted); text-decoration: none; transition: color var(--transition-fast); }
@media (hover: hover) { .breadcrumb-item:hover { color: var(--text); } }
.breadcrumb-item.current { color: var(--text); font-weight: 500; }
.breadcrumb-sep { color: var(--placeholder); font-size: 0.7rem; }
```

| Breakpoint | Sidebar |
|------------|---------|
| ≥ 900px | Fixe, 220px |
| 700–900px | Repliée en icônes (56px), tooltips |
| < 700px | Masquée, ouverture en overlay (élévation 4 + backdrop) |

Breadcrumbs : max 4 niveaux visibles, au-delà tronquer avec `…` (ouvre un dropdown des niveaux masqués).

---

## 24. Composants — Steppers & Timeline

```css
/* Stepper horizontal */
.stepper { display: flex; align-items: flex-start; }
.step { flex: 1; display: flex; flex-direction: column; align-items: center; gap: 8px; position: relative; text-align: center; }
.step:not(:last-child)::after { content: ''; position: absolute; top: 13px; left: calc(50% + 18px); right: calc(-50% + 18px); height: 2px; background: var(--border); }
.step.done:not(:last-child)::after { background: var(--accent); }
.step-dot {
  width: 26px; height: 26px; border-radius: 50%; background: var(--card2); border: 2px solid var(--border);
  color: var(--muted); display: flex; align-items: center; justify-content: center; font-size: 0.7rem; font-weight: 600; z-index: 1;
  transition: all var(--duration-normal) var(--ease-standard);
}
.step.done .step-dot    { background: var(--accent); border-color: var(--accent); color: #fff; }
.step.current .step-dot { border-color: var(--accent); color: var(--accent); box-shadow: 0 0 0 4px rgba(108, 92, 231, 0.15); }
.step-label { font-size: 0.72rem; color: var(--muted); }
.step.current .step-label { color: var(--text); font-weight: 500; }

/* Timeline verticale */
.timeline { position: relative; padding-left: 24px; }
.timeline::before { content: ''; position: absolute; left: 7px; top: 6px; bottom: 6px; width: 2px; background: var(--border); }
.timeline-item { position: relative; padding-bottom: 20px; }
.timeline-item:last-child { padding-bottom: 0; }
.timeline-dot { position: absolute; left: -24px; top: 4px; width: 16px; height: 16px; border-radius: 50%; background: var(--card); border: 2px solid var(--accent); }
.timeline-item.success .timeline-dot { border-color: var(--green); }
.timeline-item.error   .timeline-dot { border-color: var(--red); }
.timeline-item.muted   .timeline-dot { border-color: var(--placeholder); }
.timeline-time  { font-size: 0.7rem; color: var(--placeholder); font-family: var(--font-mono); }
.timeline-title { font-size: 0.85rem; font-weight: 500; margin: 2px 0; }
.timeline-text  { font-size: 0.78rem; color: var(--muted); line-height: 1.5; }
```

---

## 25. Composants — Graphiques (Chart.js)

### Configuration globale

```js
const chartDefaults = {
  backgroundColor: 'transparent',
  gridColor: '#2a2d40',   // var(--border)
  axisColor: '#7a7d90',   // var(--muted)
  axisFont: { size: 11 },
  lineColor: '#6c5ce7',   // var(--accent)
  lineTension: 0.3,
  pointRadius: 3, pointHoverRadius: 5, pointBackgroundColor: '#6c5ce7',
};
```

### Thématisation (résolution des tokens)

Les couleurs Chart.js étant définies en JS, prévoir une résolution des tokens à la bascule de thème :

```js
function chartColors() {
  const s = getComputedStyle(document.documentElement);
  return {
    grid:  s.getPropertyValue('--border').trim(),
    ticks: s.getPropertyValue('--muted').trim(),
    card:  s.getPropertyValue('--card').trim(),
    text:  s.getPropertyValue('--text').trim(),
  };
}
// À la bascule : mettre à jour options.scales.*.grid.color / ticks.color, datasets borderColor, puis chart.update()
```

### Section de graphique

```css
.chart-section { background: var(--card); border: 1px solid var(--border); border-radius: var(--radius-lg); padding: 20px; margin-bottom: 24px; position: relative; box-shadow: var(--elevation-2); }
.chart-title   { font-size: 0.85rem; color: var(--muted); margin-bottom: 12px; display: flex; align-items: center; justify-content: space-between; gap: 8px; }
.chart-container { position: relative; height: 220px; }
```

### Donut

```js
new Chart(ctx, {
  type: 'doughnut',
  data: { labels: ['A', 'B', 'C', 'D'], datasets: [{
    data: [42, 27, 19, 12],
    backgroundColor: ['#6c5ce7', '#00d4ff', '#f050a0', '#00d68f'],
    borderColor: 'var(--card)', borderWidth: 3, hoverOffset: 6,
  }]},
  options: { cutout: '68%', plugins: { legend: { position: 'bottom', labels: { color: '#7a7d90', boxWidth: 10, padding: 14, font: { size: 11 } } } } }
});
```

> Centre du donut : valeur totale en `1.4rem / 700`, label en dessous (`0.7rem`, `--muted`).

### Barres

```js
new Chart(ctx, {
  type: 'bar',
  data: { labels, datasets: [{
    data: values, backgroundColor: 'rgba(108, 92, 231, 0.75)', hoverBackgroundColor: '#6c5ce7',
    borderRadius: 5, borderSkipped: false, maxBarThickness: 32,
  }]},
  options: { plugins: { legend: { display: false } },
    scales: { x: { grid: { display: false }, ticks: { color: '#7a7d90' } }, y: { grid: { color: '#2a2d40' }, ticks: { color: '#7a7d90' } } } }
});
```

### Sparkline (mini-courbe, 40–48px)

```js
new Chart(ctx, {
  type: 'line',
  data: { labels: Array(data.length).fill(''), datasets: [{
    data, borderColor: '#00d4ff', backgroundColor: 'rgba(0, 212, 255, 0.08)',
    fill: true, tension: 0.4, pointRadius: 0, borderWidth: 2,
  }]},
  options: { plugins: { legend: { display: false }, tooltip: { enabled: false } },
    scales: { x: { display: false }, y: { display: false } }, responsive: true, maintainAspectRatio: false }
});
```

### Heatmap (CSS pur)

```css
.heatmap { display: grid; grid-template-columns: repeat(auto-fill, 14px); gap: 3px; }
.heatmap-cell { width: 14px; height: 14px; border-radius: 3px; background: var(--card2); }
.heatmap-cell.l1 { background: rgba(108, 92, 231, 0.2); }
.heatmap-cell.l2 { background: rgba(108, 92, 231, 0.4); }
.heatmap-cell.l3 { background: rgba(108, 92, 231, 0.6); }
.heatmap-cell.l4 { background: rgba(108, 92, 231, 0.8); }
.heatmap-cell.l5 { background: var(--accent); }
```

---

## 26. États système — Empty & Error

```css
/* Empty state */
.empty-state { display: flex; flex-direction: column; align-items: center; text-align: center; padding: 48px 24px; gap: 6px; }
.empty-icon { font-size: 2rem; width: 64px; height: 64px; border-radius: 50%; background: var(--card2); display: flex; align-items: center; justify-content: center; margin-bottom: 8px; }
.empty-title { font-size: 0.95rem; font-weight: 600; }
.empty-text  { font-size: 0.82rem; color: var(--muted); max-width: 320px; line-height: 1.55; }

/* Error block */
.error-block { display: flex; flex-direction: column; align-items: center; text-align: center; gap: 8px; padding: 32px 24px; border: 1px dashed var(--border); border-radius: var(--radius-lg); }
.error-block .error-title { font-size: 0.88rem; font-weight: 600; color: var(--red); }
.error-block .error-text  { font-size: 0.8rem; color: var(--muted); max-width: 320px; }
```

| Élément (empty) | Rôle | Exemple |
|---------|------|---------|
| Icône | Identifier le contexte | 📋 |
| Titre | Constater l'absence | « Aucun élément pour l'instant » |
| Texte | Expliquer quoi faire | « Les éléments créés apparaîtront ici. » |
| CTA (optionnel) | Inviter à l'action | « Créer un élément » |

**Rédaction des erreurs :** dire ce qui s'est passé et comment corriger ; pas d'excuses ni de ton dramatique ; toujours une action de sortie (« Réessayer », « Recharger »). « Une erreur est survenue » seul est interdit.

---

## 27. Page de connexion (Login)

```html
<div class="login-bg">
  <div class="orb orb-violet"></div>
  <div class="orb orb-blue"></div>
  <div class="orb orb-green"></div>
  <div class="login-card">
    <div class="login-logo">💎</div>
    <h2>Connexion</h2>
    <!-- Formulaire -->
  </div>
</div>
```

```css
.login-bg { min-height: 100vh; background: var(--grad-bg-login); display: flex; align-items: center; justify-content: center; position: relative; overflow: hidden; }

.orb { position: absolute; border-radius: 50%; filter: blur(80px); opacity: 0.15; pointer-events: none; }
.orb-violet { width: 400px; height: 400px; background: #6c5ce7; top: -100px; left: -100px; }
.orb-blue   { width: 300px; height: 300px; background: #5c8dff; bottom: -80px; right: -80px; }
.orb-green  { width: 200px; height: 200px; background: #00d68f; top: 40%; right: 10%; }

.login-card {
  background: var(--overlay); backdrop-filter: blur(20px); -webkit-backdrop-filter: blur(20px);
  border: 1px solid var(--border-subtle); border-radius: var(--radius-2xl);
  padding: 48px 40px 40px; width: 400px; max-width: 90vw; box-shadow: var(--elevation-4);
  position: relative; overflow: hidden;
}
.login-card::before { content: ''; position: absolute; top: 0; left: 0; right: 0; height: 3px; background: var(--grad-login-bar); border-radius: 0 0 3px 3px; }
.login-logo { width: 44px; height: 44px; background: var(--grad-violet-blue); border-radius: var(--radius-lg); display: flex; align-items: center; justify-content: center; font-size: 1.2rem; margin-bottom: 20px; }
```

---

## 28. Icônes & Émojis

| Contexte | Icône |
|----------|-------|
| **Favicon** | SVG violet avec `$` ou `💎` |
| **Graphique tendance** | 📈 |
| **Historique / transactions** | 📋 |
| **Statut OK / actif** | ✅ ou 🟢 |
| **Statut désactivé** | ⏭️ |
| **Erreur / alerte** | ⚠️ |
| **Chargement** | Spinner CSS (voir §8) |
| **Rafraîchir** | 🔄 |
| **Logo / Header** | 🏠 |
| **Valeur principale** | 💰 |
| **Favori** | ⭐ |

---

## 29. Breakpoints & Responsive

```css
/* Mobile — < 480px */
@media (max-width: 480px) {
  body { padding: 12px; }
  .login-card { padding: 32px 24px; }
  .card-value { font-size: 1.4rem; }
  .toast-container { left: 12px; right: 12px; max-width: none; }
}

/* Tablette — < 700px */
@media (max-width: 700px) { .charts-grid { grid-template-columns: 1fr; } }

/* Desktop compact — < 900px */
@media (max-width: 900px) { .cards-grid { grid-template-columns: repeat(auto-fit, minmax(150px, 1fr)); } }
```

---

## 30. Accessibilité

- **Contraste :** `--text` sur `--card` atteint > 4.5:1 dans les deux thèmes. Ne pas utiliser `--muted` pour du texte informatif critique.
- **Focus visible :**
  ```css
  :focus-visible { outline: 2px solid var(--accent); outline-offset: 2px; border-radius: 4px; }
  ```
- **Réduction de mouvement :**
  ```css
  @media (prefers-reduced-motion: reduce) {
    *, *::before, *::after { animation-duration: 0.01ms !important; transition-duration: 0.01ms !important; }
  }
  ```
- **ARIA :** boutons icon-only avec `aria-label` ; graphiques avec `aria-label` ou `title` ; modales `role="dialog"` + `aria-modal` ; toasts dans un conteneur `aria-live`.
- **Rôles :** `<button>` pour les actions, `<a>` pour la navigation. Pas de `<div>` cliquables.

---

## 31. Variables CSS complètes

Fichier de référence à inclure **en premier** dans votre CSS.

```css
/* =========================================
   Design Tokens — Design System (unifié)
   ========================================= */

:root {

  /* FONDS */
  --bg:              #0f1117;
  --card:            #1a1d2a;
  --card2:           #212435;
  --overlay:         rgba(26, 29, 42, 0.8);

  /* BORDURES */
  --border:          #2a2d40;
  --border-subtle:   rgba(42, 45, 64, 0.6);

  /* TEXTES */
  --text:            #e0e2f0;
  --muted:           #7a7d90;
  --placeholder:     #5a5d70;

  /* COULEURS SÉMANTIQUES */
  --accent:          #6c5ce7;
  --blue:            #5c8dff;
  --green:           #00d68f;
  --orange:          #ffa726;
  --red:             #ff5252;

  /* COULEURS ÉTENDUES */
  --pink:            #f050a0;
  --cyan:            #00d4ff;
  --teal:            #00b8a0;
  --indigo:          #4d6bfe;
  --yellow:          #f5d020;
  --lime:            #82e000;
  --purple:          #c061f7;
  --coral:           #ff6b6b;

  /* COULEURS TERTIAIRES */
  --rose:            #ff5c8a;
  --amber:           #ffc24b;
  --sky:             #38b6ff;
  --lavender:        #b09cff;
  --slate:           #8593b0;
  --magenta:         #e0399e;

  /* TYPOGRAPHIE */
  --font-ui:    -apple-system, BlinkMacSystemFont, 'Segoe UI', system-ui, sans-serif;
  --font-login: 'Inter', -apple-system, system-ui, sans-serif;
  --font-mono:  'SF Mono', 'Fira Code', 'Cascadia Code', monospace;

  /* RAYONS */
  --radius-sm:   6px;
  --radius-md:   8px;
  --radius-lg:   12px;
  --radius-xl:   16px;
  --radius-2xl:  24px;

  /* ÉLÉVATION (--shadow-* = alias) */
  --elevation-0: none;
  --elevation-1: 0 1px 3px rgba(0, 0, 0, 0.25);
  --elevation-2: 0 4px 24px rgba(0, 0, 0, 0.30);
  --elevation-3: 0 12px 40px rgba(0, 0, 0, 0.40);
  --elevation-4: 0 25px 80px rgba(0, 0, 0, 0.50);
  --shadow-card:  var(--elevation-2);
  --shadow-modal: var(--elevation-4);

  /* EASING */
  --ease-standard: ease;
  --ease-out-expo: cubic-bezier(0.16, 1, 0.3, 1);
  --ease-in-out:   cubic-bezier(0.65, 0, 0.35, 1);
  --ease-spring:   cubic-bezier(0.34, 1.56, 0.64, 1);

  /* DURÉES (--transition-* = alias) */
  --duration-instant: 0.1s;
  --duration-fast:    0.15s;
  --duration-normal:  0.2s;
  --duration-slow:    0.3s;
  --duration-overlay: 0.25s;
  --duration-toast:   0.35s;
  --transition-fast:   0.15s ease;
  --transition-normal: 0.2s ease;
  --transition-slow:   0.3s ease;

  /* DENSITÉ (défaut = normal) */
  --density-pad-y: 10px;
  --density-pad-x: 14px;
  --density-gap:   12px;

  /* DÉGRADÉS UI */
  --grad-indigo-violet:  linear-gradient(90deg,  #4d6bfe, #6c5ce7);
  --grad-orange-red:     linear-gradient(90deg,  #ffa726, #ff7043);
  --grad-blue-sky:       linear-gradient(90deg,  #5c8dff, #42a5f5);
  --grad-green:          linear-gradient(90deg,  #00d68f, #00e676);
  --grad-pink-purple:    linear-gradient(90deg,  #f050a0, #c061f7);
  --grad-cyan-teal:      linear-gradient(90deg,  #00d4ff, #00b8a0);
  --grad-lime-green:     linear-gradient(90deg,  #82e000, #00d68f);
  --grad-purple-violet:  linear-gradient(90deg,  #e040fb, #7c4dff);
  --grad-coral-orange:   linear-gradient(90deg,  #ff6b6b, #ffa726);
  --grad-yellow-orange:  linear-gradient(90deg,  #feca57, #ff9f43);
  --grad-violet-blue:    linear-gradient(135deg, #6c5ce7, #5c8dff);
  --grad-rose-amber:     linear-gradient(90deg,  #ff5c8a, #ffc24b);
  --grad-sky-lavender:   linear-gradient(90deg,  #38b6ff, #b09cff);
  --grad-magenta-rose:   linear-gradient(90deg,  #e0399e, #ff5c8a);
  --grad-login-bar:      linear-gradient(90deg,  #6c5ce7, #00d68f, #5c8dff);

  /* DÉGRADÉS DE FOND */
  --grad-bg-login:       linear-gradient(135deg, #0f1117, #1a1d2a, #0f1117);
}

/* === DENSITÉ === */
html[data-density="compact"]     { --density-pad-y: 6px;  --density-pad-x: 10px; --density-gap: 8px;  }
html[data-density="comfortable"] { --density-pad-y: 14px; --density-pad-x: 18px; --density-gap: 16px; }

/* === THÈME CLAIR === */
html[data-theme="light"] {
  color-scheme: light;

  --bg:          #f4f5fa;
  --card:        #ffffff;
  --card2:       #eef0f7;
  --overlay:     rgba(255, 255, 255, 0.82);

  --border:        #dfe2ee;
  --border-subtle: rgba(223, 226, 238, 0.6);

  --text:        #1c1e2b;
  --muted:       #6a6d82;
  --placeholder: #9a9db0;

  /* Sémantiques — variantes contrastées */
  --blue:   #3d6fe0;
  --green:  #00a371;
  --orange: #d97f00;
  --red:    #e03131;

  /* Étendues — variantes contrastées */
  --pink:   #d6328e;
  --cyan:   #0096c7;
  --teal:   #00897b;
  --yellow: #b08900;
  --lime:   #5da000;
  --purple: #9c3fd0;
  --coral:  #e05555;

  /* Tertiaires — variantes contrastées */
  --rose:     #e03f6e;
  --amber:    #c98a00;
  --sky:      #1f8fe0;
  --lavender: #7c5cf0;
  --slate:    #5a6685;
  --magenta:  #c42d86;

  /* Élévation */
  --elevation-1: 0 1px 3px rgba(20, 24, 50, 0.08);
  --elevation-2: 0 4px 24px rgba(20, 24, 50, 0.08);
  --elevation-3: 0 12px 40px rgba(20, 24, 50, 0.12);
  --elevation-4: 0 25px 80px rgba(20, 24, 50, 0.18);

  /* Fond login */
  --grad-bg-login: linear-gradient(135deg, #f4f5fa, #ffffff, #f4f5fa);
}
```

---

*Charte maintenue manuellement — toute modification doit être répercutée dans l'ensemble des fichiers source utilisant ces tokens, ainsi que dans la preview HTML associée.*
