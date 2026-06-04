# 🎨 Charte Graphique — Design System

> **Version unifiée** — Référence unique pour tous les dashboards de l'écosystème.

---

## Table des matières

1. [Tokens de design](#1-tokens-de-design)
2. [Palette de couleurs](#2-palette-de-couleurs)
3. [Dégradés](#3-dégradés)
4. [Typographie](#4-typographie)
5. [Espacements & Layout](#5-espacements--layout)
6. [Composants — Cartes](#6-composants--cartes)
7. [Composants — Boutons](#7-composants--boutons)
8. [Composants — Tableaux](#8-composants--tableaux)
9. [Composants — Badges](#9-composants--badges)
10. [Composants — Formulaires & Inputs](#10-composants--formulaires--inputs)
11. [Composants — Graphiques (Chart.js)](#11-composants--graphiques-chartjs)
12. [Page de connexion (Login)](#12-page-de-connexion-login)
13. [Animations & Transitions](#13-animations--transitions)
14. [Icônes & Émojis](#14-icônes--émojis)
15. [Breakpoints & Responsive](#15-breakpoints--responsive)
16. [Accessibilité](#16-accessibilité)
17. [Variables CSS complètes](#17-variables-css-complètes)

---

## 1. Tokens de design

Les tokens sont les briques atomiques de l'interface. Tout composant doit **exclusivement** référencer ces variables — aucune valeur codée en dur dans les composants.

```css
:root {
  /* === FONDS === */
  --bg:          #0f1117;   /* Fond principal de la page */
  --card:        #1a1d2a;   /* Fond des cartes et sections */
  --card2:       #212435;   /* Fond des contrôles (inputs, selects, boutons secondaires) */
  --overlay:     rgba(26, 29, 42, 0.8); /* Fond semi-transparent (glassmorphism) */

  /* === BORDURES === */
  --border:      #2a2d40;   /* Bordure standard */
  --border-subtle: rgba(42, 45, 64, 0.6); /* Bordure sur fond transparent */

  /* === TEXTES === */
  --text:        #e0e2f0;   /* Texte principal */
  --muted:       #7a7d90;   /* Texte secondaire (labels, sous-titres) */
  --placeholder: #5a5d70;   /* Texte fantôme, statuts désactivés */

  /* === COULEURS SÉMANTIQUES === */
  --accent:      #6c5ce7;   /* Violet — accent principal */
  --blue:        #5c8dff;   /* Bleu — balance, information */
  --green:       #00d68f;   /* Vert — succès, tendance positive */
  --orange:      #ffa726;   /* Orange — attention, consommation */
  --red:         #ff5252;   /* Rouge — erreur, tendance négative */

  /* === COULEURS ÉTENDUES === */
  --pink:        #f050a0;   /* Rose vif — highlight, nouveauté, promo */
  --cyan:        #00d4ff;   /* Cyan électrique — données temps réel, live */
  --teal:        #00b8a0;   /* Teal — indicateurs neutres, tags secondaires */
  --indigo:      #4d6bfe;   /* Indigo — variante sombre de l'accent */
  --yellow:      #f5d020;   /* Jaune — avertissement doux, mise en avant */
  --lime:        #82e000;   /* Lime — performance, score élevé */
  --purple:      #c061f7;   /* Violet clair — labels secondaires, catégories */
  --coral:       #ff6b6b;   /* Corail — alertes douces, erreurs non critiques */

  /* === RAYONS === */
  --radius-sm:   6px;
  --radius-md:   8px;
  --radius-lg:   12px;
  --radius-xl:   16px;
  --radius-2xl:  24px;

  /* === OMBRES === */
  --shadow-card:  0 4px 24px rgba(0, 0, 0, 0.3);
  --shadow-modal: 0 25px 80px rgba(0, 0, 0, 0.5);

  /* === TRANSITIONS === */
  --transition-fast:   0.15s ease;
  --transition-normal: 0.2s ease;
  --transition-slow:   0.3s ease;
}
```

---

## 2. Palette de couleurs

| Rôle | Nom | Token | Hex |
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

#### Palette étendue

| Rôle | Nom | Token | Hex |
|------|-----|-------|-----|
| **Rose vif** | Highlight / nouveauté | `--pink` | `#f050a0` |
| **Cyan électrique** | Live / temps réel | `--cyan` | `#00d4ff` |
| **Teal** | Tags neutres / secondaires | `--teal` | `#00b8a0` |
| **Indigo** | Accent sombre | `--indigo` | `#4d6bfe` |
| **Jaune** | Avertissement doux | `--yellow` | `#f5d020` |
| **Lime** | Performance / score élevé | `--lime` | `#82e000` |
| **Violet clair** | Labels / catégories | `--purple` | `#c061f7` |
| **Corail** | Alerte douce | `--coral` | `#ff6b6b` |

> Les couleurs de la palette étendue viennent **compléter** la palette sémantique — elles ne la remplacent pas. Elles servent principalement pour les graphiques multi-séries, les tags, les catégories, et les indicateurs supplémentaires.

### Usage sémantique des couleurs

| Contexte | Couleur recommandée |
|----------|---------------------|
| Balance / crédit disponible | `--blue` |
| Consommation / dépense | `--orange` |
| Statut API actif, tendance positive | `--green` |
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

### Ordre recommandé pour graphiques multi-séries

Quand plusieurs séries de données cohabitent sur un même graphique, utiliser cet ordre pour maximiser la distinction visuelle :

```
1. --accent  #6c5ce7  Violet
2. --cyan    #00d4ff  Cyan
3. --pink    #f050a0  Rose
4. --green   #00d68f  Vert
5. --yellow  #f5d020  Jaune
6. --blue    #5c8dff  Bleu
7. --coral   #ff6b6b  Corail
8. --lime    #82e000  Lime
9. --purple  #c061f7  Violet clair
10. --teal   #00b8a0  Teal
```

---

## 3. Dégradés

> **Convention de nommage :** `--grad-[couleur1]-[couleur2]` basé sur les couleurs dominantes. Les dégradés destinés exclusivement aux fonds d'écran utilisent le préfixe `--grad-bg-`.

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
| `--grad-login-bar` | Violet → Vert → Bleu | `linear-gradient(90deg, #6c5ce7, #00d68f, #5c8dff)` |

### Dégradés de fond (`--grad-bg-*`)

| Variable | Description | Valeur |
|----------|-------------|--------|
| `--grad-bg-login` | Fond pleine page login | `linear-gradient(135deg, #0f1117, #1a1d2a, #0f1117)` |

### Matrice d'usages courants

| Variable | Barre top tuile | Texte tuile | Courbe chart | Bouton | Badge |
|----------|:-:|:-:|:-:|:-:|:-:|
| `--grad-indigo-violet` | ✅ | ✅ | ✅ | ✅ | ✅ |
| `--grad-orange-red` | ✅ | ✅ | ✅ | ✅ | ✅ |
| `--grad-blue-sky` | ✅ | ✅ | ✅ | ✅ | ✅ |
| `--grad-green` | ✅ | ✅ | ✅ | ✅ | ✅ |
| `--grad-pink-purple` | ✅ | ✅ | ✅ | ✅ | ✅ |
| `--grad-cyan-teal` | ✅ | ✅ | ✅ | ✅ | ✅ |
| `--grad-lime-green` | ✅ | ✅ | ✅ | ✅ | ✅ |
| `--grad-purple-violet` | ✅ | ✅ | ✅ | ✅ | ✅ |
| `--grad-coral-orange` | ✅ | ✅ | ✅ | ✅ | ✅ |
| `--grad-yellow-orange` | ✅ | ✅ | ✅ | ✅ | ✅ |
| `--grad-violet-blue` | ✅ | ✅ | ✅ | ✅ | ✅ |
| `--grad-login-bar` | ✅ | ✅ | ✅ | ✅ | ✅ |

---

## 4. Typographie

### Familles de polices

```css
/* Interface principale */
--font-ui: -apple-system, BlinkMacSystemFont, 'Segoe UI', system-ui, sans-serif;

/* Page de login (charge depuis Google Fonts) */
--font-login: 'Inter', -apple-system, system-ui, sans-serif;

/* Code, valeurs techniques (tokens, IDs…) */
--font-mono: 'SF Mono', 'Fira Code', 'Cascadia Code', monospace;
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
| **Monospace** | `0.8rem` | `400` | Pour valeurs techniques |

---

## 5. Espacements & Layout

### Système d'espacement (base 4px)

```
4px  — espacement micro (entre badge et texte)
8px  — espacement XS (padding boutons compacts)
12px — espacement SM (padding mobile, gap interne)
16px — espacement MD (gap de grille cartes)
20px — espacement LG (padding carte, padding page)
24px — espacement XL (margin entre sections)
30px — espacement 2XL (margin header)
48px — espacement 3XL (padding carte login)
```

### Layout général

```css
body {
  padding: 20px;        /* 12px sur mobile */
  background: var(--bg);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
}

.cards-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 16px;
}

.charts-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 16px;
}
```

---

## 6. Composants — Cartes

### Structure de base

```css
.card {
  background: var(--card);
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);   /* 12px */
  padding: 20px;
  position: relative;
  overflow: hidden;
  box-shadow: var(--shadow-card);
  transition: border-color var(--transition-normal);
}

.card:hover {
  border-color: rgba(108, 92, 231, 0.35);
}

/* Barre colorée en haut — à spécialiser par classe */
.card::before {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0;
  height: 3px;
}
```

### Spécialisations par type

```css
.card.card-1::before     { background: var(--grad-indigo-violet); }
.card.consumption::before { background: var(--grad-orange-red); }
.card.card-3::before   { background: var(--grad-blue-sky); }
.card.card-4::before  { background: var(--grad-green); }
.card.rhythm::before      { background: var(--grad-purple-violet); }
.card.live::before        { background: var(--grad-cyan-teal); }
.card.highlight::before   { background: var(--grad-pink-purple); }
.card.performance::before { background: var(--grad-lime-green); }
.card.alert-soft::before  { background: var(--grad-coral-orange); }
```

### Contenu interne

```css
.card-label {
  font-size: 0.75rem;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: var(--muted);
  margin-bottom: 6px;
}

.card-value {
  font-size: 1.8rem;
  font-weight: 700;
  line-height: 1.2;
}

/* Variantes de couleur pour .card-value */
.card-value.green {
  background: linear-gradient(90deg, #00d68f, #00e676);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}
.card-value.orange {
  background: linear-gradient(90deg, #ffa726, #ff7043);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}
.card-value.blue {
  background: linear-gradient(90deg, #5c8dff, #42a5f5);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}
.card-value.accent {
  background: linear-gradient(90deg, #4d6bfe, #6c5ce7);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}

.card-sub {
  font-size: 0.8rem;
  color: var(--muted);
  margin-top: 4px;
}
```

### Tuiles statistiques (variante compacte, barre 2px)

```css
.stat-tile {
  position: relative;
  overflow: hidden;
  background: var(--card);
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);
  padding: 16px 20px;
}

.stat-tile::before {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0;
  height: 2px;
}

.stat-tile:nth-child(1)::before { background: var(--grad-coral-orange); }  /* Tuile 1 */
.stat-tile:nth-child(2)::before { background: var(--grad-cyan-teal); }      /* Tendance */
.stat-tile:nth-child(3)::before { background: var(--grad-yellow-orange); }  /* Moyenne 7j */
.stat-tile:nth-child(4)::before { background: var(--grad-indigo-violet); }  /* Tuile 4 */
```

---

## 7. Composants — Boutons

> **⚠️ Règle tactile :** Tous les états `:hover` sur les boutons interactifs (navigation, pagination, filtres, scroll) sont protégés par `@media (hover: hover)` pour éviter le "stuck hover" sur écran tactile.

### Bouton secondaire (header, contrôles)

```css
.btn {
  background: var(--card2);
  color: var(--text);
  border: 1px solid var(--border);
  padding: 8px 16px;
  border-radius: var(--radius-md);
  cursor: pointer;
  font-size: 0.85rem;
  font-family: var(--font-ui);
  transition: all var(--transition-normal);
  white-space: nowrap;
}

@media (hover: hover) {
  .btn:hover {
    background: linear-gradient(135deg, #6c5ce7, #5c8dff);
    border-color: var(--accent);
    color: #fff;
  }
}

.btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
```

### Bouton primaire (login, actions principales)

```css
.btn-primary {
  width: 100%;
  padding: 12px 20px;
  background: var(--grad-violet-blue);
  border: none;
  border-radius: 10px;
  color: #fff;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all var(--transition-normal);
}

.btn-primary:hover {
  background: #7c6cf0;
  transform: translateY(-1px);
  box-shadow: 0 8px 24px rgba(108, 92, 231, 0.4);
}

.btn-primary:active {
  transform: translateY(0);
}
```

### Boutons filtres (1h / 1j / 7j / 30j)

```css
.filter-btn {
  padding: 4px 10px;
  background: var(--card2);
  border: 1px solid var(--border);
  border-radius: var(--radius-sm);
  color: var(--muted);
  font-size: 0.75rem;
  cursor: pointer;
  transition: all var(--transition-fast);
}

@media (hover: hover) {
  .filter-btn:hover {
    background: linear-gradient(135deg, #6c5ce7, #5c8dff);
    border-color: var(--accent);
    color: #fff;
  }
}

.filter-btn.active {
  background: linear-gradient(135deg, #6c5ce7, #5c8dff);
  border-color: var(--accent);
  color: #fff;
}
```

### Boutons de pagination

```css
/* Numéro de page */
.pag-page {
  padding: 4px 8px;
  min-width: 30px;
  text-align: center;
  background: var(--card2);
  border: 1px solid var(--border);
  border-radius: var(--radius-sm);
  color: var(--muted);
  font-size: 0.75rem;
  cursor: pointer;
  line-height: 1.4;
  transition: all var(--transition-fast);
}

@media (hover: hover) {
  .pag-page:hover {
    background: linear-gradient(135deg, #6c5ce7, #5c8dff);
    border-color: var(--accent);
    color: #fff;
  }
}

.pag-page.active {
  background: linear-gradient(135deg, #6c5ce7, #5c8dff);
  border-color: var(--accent);
  color: #fff;
}

.pag-page.dots {
  background: none;
  border: none;
  cursor: default;
  color: var(--muted);
  min-width: auto;
}

/* Boutons navigation et taille de page */
.nav-btn,
.pag-btn {
  padding: 5px 8px;
  background: var(--card2);
  border: 1px solid var(--border);
  border-radius: var(--radius-sm);
  color: var(--muted);
  font-size: 0.75rem;
  cursor: pointer;
  line-height: 1;
  transition: all var(--transition-fast);
}

@media (hover: hover) {
  .nav-btn:hover,
  .pag-btn:hover {
    background: linear-gradient(135deg, #6c5ce7, #5c8dff);
    border-color: var(--accent);
    color: #fff;
  }
}

.nav-btn.active,
.pag-btn.active {
  background: linear-gradient(135deg, #6c5ce7, #5c8dff);
  border-color: var(--accent);
  color: #fff;
}
```

### Boutons de scroll graphique (◀ ▶)

```css
.scroll-btn {
  position: absolute;
  top: 55%;
  transform: translateY(-50%);
  z-index: 10;
  background: var(--card2);
  border: 1px solid var(--border);
  border-radius: var(--radius-sm);
  color: var(--muted);
  font-size: 0.7rem;
  cursor: pointer;
  padding: 6px 5px;
  display: none;
  line-height: 1;
  transition: all var(--transition-fast);
}

@media (hover: hover) {
  .scroll-btn:hover {
    background: linear-gradient(135deg, #6c5ce7, #5c8dff);
    border-color: var(--accent);
    color: #fff;
  }
}
```

---

## 8. Composants — Tableaux

```css
.table-wrap {
  background: var(--card);
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);
  overflow-x: auto;
  margin-bottom: 24px;
}

table {
  width: 100%;
  border-collapse: collapse;
  font-size: 0.85rem;
}

th {
  text-align: left;
  padding: 10px 12px;
  color: var(--muted);
  font-weight: 500;
  border-bottom: 1px solid var(--border);
  white-space: nowrap;
}

td {
  padding: 9px 12px;
  border-bottom: 1px solid var(--border);
  color: var(--text);
  vertical-align: middle;
}

tr:last-child td {
  border: none;
}

/* Ligne au survol */
@media (hover: hover) {
  tbody tr:hover td {
    background: rgba(108, 92, 231, 0.05);
  }
}

/* Cellule avec valeur monospace (IDs, clés) */
td.mono {
  font-family: var(--font-mono);
  font-size: 0.8rem;
  color: var(--muted);
}
```

---

## 9. Composants — Badges

```css
.badge {
  display: inline-flex;
  align-items: center;
  gap: 4px;
  padding: 2px 8px;
  border-radius: 4px;
  font-size: 0.75rem;
  font-weight: 500;
  line-height: 1.6;
}

.badge.green  {
  background: rgba(0, 214, 143, 0.15);
  color: var(--green);
}
.badge.red    {
  background: rgba(255, 82, 82, 0.15);
  color: var(--red);
}
.badge.orange {
  background: rgba(255, 167, 38, 0.15);
  color: var(--orange);
}
.badge.blue   {
  background: rgba(92, 141, 255, 0.15);
  color: var(--blue);
}
.badge.accent {
  background: rgba(108, 92, 231, 0.15);
  color: var(--accent);
}
.badge.muted  {
  background: rgba(122, 125, 144, 0.15);
  color: var(--muted);
}
/* Palette étendue */
.badge.pink   {
  background: rgba(240, 80, 160, 0.15);
  color: var(--pink);
}
.badge.cyan   {
  background: rgba(0, 212, 255, 0.15);
  color: var(--cyan);
}
.badge.teal   {
  background: rgba(0, 184, 160, 0.15);
  color: var(--teal);
}
.badge.indigo {
  background: rgba(77, 107, 254, 0.15);
  color: var(--indigo);
}
.badge.yellow {
  background: rgba(245, 208, 32, 0.15);
  color: var(--yellow);
}
.badge.lime   {
  background: rgba(130, 224, 0, 0.15);
  color: var(--lime);
}
.badge.purple {
  background: rgba(192, 97, 247, 0.15);
  color: var(--purple);
}
.badge.coral  {
  background: rgba(255, 107, 107, 0.15);
  color: var(--coral);
}
```

---

## 10. Composants — Formulaires & Inputs

```css
.input-group {
  display: flex;
  flex-direction: column;
  gap: 6px;
  margin-bottom: 16px;
}

.input-label {
  font-size: 0.8rem;
  font-weight: 500;
  color: var(--muted);
  letter-spacing: 0.03em;
}

.input {
  background: rgba(15, 17, 23, 0.6);
  border: 1px solid var(--border);
  border-radius: 10px;
  padding: 11px 14px;
  color: var(--text);
  font-size: 0.9rem;
  font-family: var(--font-ui);
  transition: border-color var(--transition-normal), box-shadow var(--transition-normal);
  outline: none;
  width: 100%;
  box-sizing: border-box;
}

.input::placeholder {
  color: var(--placeholder);
}

.input:focus {
  border-color: var(--accent);
  box-shadow: 0 0 0 3px rgba(108, 92, 231, 0.2);
}

.input:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

/* Select */
select.input {
  cursor: pointer;
  appearance: none;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='12' viewBox='0 0 12 12'%3E%3Cpath fill='%237a7d90' d='M6 8L1 3h10z'/%3E%3C/svg%3E");
  background-repeat: no-repeat;
  background-position: right 12px center;
  padding-right: 32px;
}
```

---

## 11. Composants — Graphiques (Chart.js)

### Configuration globale recommandée

```js
const chartDefaults = {
  // Fond transparent — laisse voir le fond .chart-section
  backgroundColor: 'transparent',

  // Grille
  gridColor: '#2a2d40',        // var(--border)

  // Axes
  axisColor: '#7a7d90',        // var(--muted)
  axisFont: { size: 11 },

  // Courbe principale
  lineColor: '#6c5ce7',        // var(--accent)
  lineTension: 0.3,

  // Points
  pointRadius: 3,
  pointHoverRadius: 5,
  pointBackgroundColor: '#6c5ce7',
};
```

### Configuration Chart.js typique

```js
const options = {
  responsive: true,
  maintainAspectRatio: false,
  plugins: {
    legend: { display: false },
    tooltip: {
      backgroundColor: '#1a1d2a',
      borderColor: '#2a2d40',
      borderWidth: 1,
      titleColor: '#e0e2f0',
      bodyColor: '#7a7d90',
      padding: 10,
      cornerRadius: 8,
    },
  },
  scales: {
    x: {
      grid: { color: '#2a2d40' },
      ticks: { color: '#7a7d90', font: { size: 11 } },
    },
    y: {
      grid: { color: '#2a2d40' },
      ticks: { color: '#7a7d90', font: { size: 11 } },
    },
  },
};
```

### Section contenant un graphique

```css
.chart-section {
  background: var(--card);
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);
  padding: 20px;
  margin-bottom: 24px;
  position: relative;
}

.chart-title {
  font-size: 0.85rem;
  color: var(--muted);
  margin-bottom: 12px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 8px;
}

.chart-container {
  position: relative;
  height: 220px;
}
```

---

## 12. Page de connexion (Login)

### Structure HTML

```html
<div class="login-bg">
  <!-- Orbes décoratifs -->
  <div class="orb orb-violet"></div>
  <div class="orb orb-blue"></div>
  <div class="orb orb-green"></div>

  <!-- Carte de login -->
  <div class="login-card">
    <div class="login-logo">💎</div>
    <h2>Connexion</h2>
    <!-- Formulaire ici -->
  </div>
</div>
```

### CSS login

```css
.login-bg {
  min-height: 100vh;
  background: linear-gradient(135deg, #0f1117, #1a1d2a, #0f1117);
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  overflow: hidden;
}

/* Orbes d'arrière-plan */
.orb {
  position: absolute;
  border-radius: 50%;
  filter: blur(80px);
  opacity: 0.15;
  pointer-events: none;
}
.orb-violet { width: 400px; height: 400px; background: #6c5ce7; top: -100px; left: -100px; }
.orb-blue   { width: 300px; height: 300px; background: #5c8dff; bottom: -80px; right: -80px; }
.orb-green  { width: 200px; height: 200px; background: #00d68f; top: 40%; right: 10%; }

/* Carte glassmorphism */
.login-card {
  background: rgba(26, 29, 42, 0.8);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border: 1px solid rgba(42, 45, 64, 0.6);
  border-radius: var(--radius-2xl);  /* 24px */
  padding: 48px 40px 40px;
  width: 400px;
  max-width: 90vw;
  box-shadow: var(--shadow-modal);
  position: relative;
  overflow: hidden;
}

/* Barre tricolore en haut de la carte */
.login-card::before {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0;
  height: 3px;
  background: var(--grad-login-bar);
  border-radius: 0 0 3px 3px;
}

/* Logo */
.login-logo {
  width: 44px;
  height: 44px;
  background: linear-gradient(135deg, #6c5ce7, #5c8dff);
  border-radius: var(--radius-lg);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.2rem;
  margin-bottom: 20px;
}
```

---

## 13. Animations & Transitions

### Règles globales

```css
/* Toutes les transitions utilisent les tokens --transition-* */
* {
  transition-timing-function: ease;
}
```

### Loader spinner

```css
.loader {
  width: 20px;
  height: 20px;
  border: 2px solid var(--border);
  border-top-color: var(--accent);
  border-radius: 50%;
  animation: spin 0.7s linear infinite;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}
```

### Apparition de carte (page load)

```css
.card {
  animation: fadeUp 0.3s ease both;
}

.card:nth-child(1) { animation-delay: 0.05s; }
.card:nth-child(2) { animation-delay: 0.10s; }
.card:nth-child(3) { animation-delay: 0.15s; }
.card:nth-child(4) { animation-delay: 0.20s; }

@keyframes fadeUp {
  from {
    opacity: 0;
    transform: translateY(12px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
```

### Pulse (statut actif)

```css
.status-pulse {
  display: inline-block;
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: var(--green);
  animation: pulse 2s ease infinite;
}

@keyframes pulse {
  0%, 100% { opacity: 1; transform: scale(1); }
  50%       { opacity: 0.5; transform: scale(0.85); }
}
```

### Récapitulatif des durées

| Interaction | Durée | Token |
|-------------|-------|-------|
| Hover bouton / badge | `0.15s` | `--transition-fast` |
| Hover carte, focus input | `0.2s` | `--transition-normal` |
| Courbe Chart.js | `0.3s` | `--transition-slow` |
| Loader | `0.7s` | — (infini) |
| Pulse statut | `2s` | — (infini) |

---

## 14. Icônes & Émojis

| Contexte | Icône |
|----------|-------|
| **Favicon** | SVG violet avec `$` ou `💎` |
| **Graphique tendance** | 📈 |
| **Historique / transactions** | 📋 |
| **Statut OK / API actif** | ✅ ou 🟢 |
| **Statut désactivé** | ⏭️ |
| **Erreur / alerte** | ⚠️ |
| **Chargement** | Spinner CSS (voir [Animations](#13-animations--transitions)) |
| **Rafraîchir** | 🔄 |
| **Logo / Header** | 🏠 (Logo application) |
| **Valeur principale** | 💰 |

---

## 15. Breakpoints & Responsive

```css
/* Mobile — < 480px */
@media (max-width: 480px) {
  body { padding: 12px; }
  .login-card { padding: 32px 24px; }
  .card-value { font-size: 1.4rem; }
}

/* Tablette — < 700px */
@media (max-width: 700px) {
  .charts-grid {
    grid-template-columns: 1fr;
  }
}

/* Desktop compact — < 900px */
@media (max-width: 900px) {
  .cards-grid {
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  }
}
```

---

## 16. Accessibilité

### Règles minimales à respecter

- **Contraste :** Le texte `--text` sur fond `--card` atteint un ratio > 4.5:1. Ne pas utiliser `--muted` pour du texte informatif critique.
- **Focus visible :** Tous les éléments interactifs doivent avoir un `focus-visible` explicite.
  ```css
  :focus-visible {
    outline: 2px solid var(--accent);
    outline-offset: 2px;
    border-radius: 4px;
  }
  ```
- **Réduction de mouvement :** Respecter la préférence système.
  ```css
  @media (prefers-reduced-motion: reduce) {
    *, *::before, *::after {
      animation-duration: 0.01ms !important;
      transition-duration: 0.01ms !important;
    }
  }
  ```
- **Attributs ARIA :** Les boutons icon-only doivent avoir `aria-label`. Les graphiques doivent avoir un `aria-label` ou `title`.
- **Rôles :** Utiliser des `<button>` pour les actions, `<a>` pour la navigation. Ne pas utiliser `<div>` cliquables.

---

## 17. Variables CSS complètes

Fichier de référence à inclure en premier dans votre CSS :

```css
/* =========================================
   Design Tokens — Design System
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

  /* TYPOGRAPHIE */
  --font-ui:   -apple-system, BlinkMacSystemFont, 'Segoe UI', system-ui, sans-serif;
  --font-mono: 'SF Mono', 'Fira Code', 'Cascadia Code', monospace;

  /* RAYONS */
  --radius-sm:   6px;
  --radius-md:   8px;
  --radius-lg:   12px;
  --radius-xl:   16px;
  --radius-2xl:  24px;

  /* OMBRES */
  --shadow-card:   0 4px 24px rgba(0, 0, 0, 0.3);
  --shadow-modal:  0 25px 80px rgba(0, 0, 0, 0.5);

  /* TRANSITIONS */
  --transition-fast:   0.15s ease;
  --transition-normal: 0.2s ease;
  --transition-slow:   0.3s ease;

  /* DÉGRADÉS UI — tuiles, textes, boutons, badges, courbes */
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
  --grad-login-bar:      linear-gradient(90deg,  #6c5ce7, #00d68f, #5c8dff);

  /* DÉGRADÉS DE FOND — exclusivement pour les arrière-plans de page */
  --grad-bg-login:       linear-gradient(135deg, #0f1117, #1a1d2a, #0f1117);
}
```

---

*Charte maintenue manuellement — toute modification doit être répercutée dans l'ensemble des fichiers source utilisant ces tokens.*
