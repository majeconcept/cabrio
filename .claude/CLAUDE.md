# CABRIO — Brasserie Artisanale d'Alsace

## Architecture

- Site vitrine single-page vanilla HTML/CSS/JS (pas de framework, pas de build step)
- 3 fichiers HTML principaux :
  - `index.html` — Landing page publique (bières, aventure, contact, revendeurs)
  - `pro.html` — Espace revendeurs B2B (catalogue, commande, historique, consignes, tarifs)
  - `admin.html` — ERP/CRM interne (commandes, clients, consignes, livraisons, produits)

## Stack technique

- HTML/CSS/JS vanilla uniquement
- CSS custom properties pour le design system
- `sessionStorage` pour l'authentification (code d'accès)
- `localStorage` pour la persistance des données (commandes, clients, consignes, livraisons)
- EmailJS SDK pour l'envoi de commandes par email (avec fallback mailto)
- Google Maps embed pour la localisation
- Images en `.webp` (avec fallback `.png`)

## Produits

13 produits : 12 bières + Slimo (limonade artisanale)

### Tarifs PRO HT 2026 (prix unitaires, droits acquittés)

Les prix varient par produit. Fourchette : 33cl de 1.55€ à 1.99€, 75cl de 3.75€ à 4.14€.
Les prix par lot sont calculés automatiquement (prix unitaire x quantité du lot).

### Formats de conditionnement

| ID | Format | Calcul |
|-----|-----|------|
| 33u | 33cl Unité | prix unitaire 33cl |
| 33c | 33cl Carton de 12 | 12 x prix unitaire 33cl |
| 75u | 75cl Unité | prix unitaire 75cl |
| 75c | 75cl Carton de 6 | 6 x prix unitaire 75cl |
| 75c12 | 75cl Caisse CFP 12 (consignée 5€) | 12 x prix unitaire 75cl |
| f20 | Fût 20L (consigné 30€) | 85.00€ fixe |
| f30 | Fût 30L (consigné 30€) | 120.00€ fixe |

### Packs spéciaux
- Tripack 3x33cl : 6.76€ HT
- Sixpack 6x33cl : 12.28€ HT
- Sixpack Noël 6x33cl : 14.10€ HT

### Conditions commerciales
- TVA 20% (5.5% limonade)
- Paiement 30 jours net
- Franco de port dès 850€ HT/commande
- Validité tarifs : 31/12/2026
- Facturation en droits acquittés

## Codes d'accès

- **Revendeurs (pro.html)** : `CABRIO-PRO-2024`, `CABRIOPRO`, `PRO2024`
- **Admin (admin.html)** : `CABRIO-ADMIN-2024`, `admin`

## localStorage keys

- `cabrio_pro_orders` — Commandes côté revendeur
- `cabrio_pro_deposits` — Consignes côté revendeur
- `cabrio_admin_orders` — Commandes côté admin
- `cabrio_admin_clients` — Clients CRM
- `cabrio_admin_deposits` — Consignes côté admin
- `cabrio_admin_deliveries` — Livraisons

## Images

- Les bouteilles sont dans `images/` avec le pattern `{Nom} bouteille.webp`
- Attention aux underscores dans certains noms de fichiers :
  - `L'Hermine Épices Noel_bouteille.webp` (underscore avant "bouteille")
  - `Boreale Kveik _bouteille.webp` (espace + underscore avant "bouteille")
  - `Slimo_bouteille.webp` (underscore)
- `FAVICON.svg` — Logo chèvre/houblon utilisé comme élément décoratif dans les cartes (via CSS mask-image)

## Design

- Font display : Bebas Neue
- Font body : Inter
- Couleurs principales : `--dark: #1a1713`, `--cream: #F5EDD8`, `--amber: #D4881C`
- Chaque bière a sa propre `--beer-color` en CSS custom property
- Cartes bières : `border-radius: 22px`, `overflow: hidden`
- Hover des cartes : fond passe en dark, favicon prend la couleur de la bière

## Localisation

Brasserie CABRIO — 4 rue des Fabriques, 68470 Fellering, Alsace
Coordonnées GPS : 47.8867408, 6.9944701

## Déploiement

- GitHub : `majeconcept/cabrio` (branche `main`)
- Push direct sur main
- Le user communique en français

## Preview server

```json
{
  "name": "cabrio-site",
  "runtimeExecutable": "npx",
  "runtimeArgs": ["serve", "-l", "8080", "/Users/Max/Library/Mobile Documents/com~apple~CloudDocs/CLAUDE/CABRIO"],
  "port": 8080
}
```

## TODO futur

- Configurer les vrais credentials EmailJS (actuellement placeholders)
- Connecter les données pro.html ↔ admin.html (actuellement localStorage séparés)
- Fonctionnalités additionnelles selon les besoins du user
