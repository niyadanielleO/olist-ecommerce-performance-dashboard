# Guide de construction du dashboard dans Tableau Public

Ce guide décrit pas à pas la construction du tableau de bord à partir des deux fichiers produits par le notebook `01_preparation_tableau.ipynb` :
- `outputs/tableau_commandes.csv` (une ligne par commande)
- `outputs/tableau_articles.csv` (une ligne par article vendu)

Les libellés sont donnés tels qu'ils apparaissent dans Tableau Public Desktop en anglais, avec l'équivalent français entre parenthèses.

---

## 0. Préparer Tableau Public

1. Créer un compte gratuit sur https://public.tableau.com.
2. Télécharger et installer **Tableau Public Desktop** (compatible Mac).
3. Ouvrir Tableau Public Desktop et se connecter avec son compte.

## 1. Se connecter aux données

1. Écran d'accueil, colonne **Connect** (Se connecter) : **To a File > Text file** (Fichier texte).
2. Choisir `outputs/tableau_commandes.csv`.
3. Dans l'aperçu, vérifier les types (icône au-dessus de chaque colonne) :
   - `date_achat` : **Date**
   - `etat_client` : cliquer sur l'icône, puis **Geographic Role > State/Province** (Rôle géographique > État/Province)
   - `chiffre_affaires`, `frais_port`, `note`, `delai_livraison_jours`, `retard_jours` : **Number (decimal)** ou **Number (whole)**
4. Ajouter la seconde source : menu **Data > New Data Source** (Données > Nouvelle source de données) > **Text file** > `outputs/tableau_articles.csv`.
5. Renommer les sources (clic droit dans le volet Données > **Rename**) : `Commandes` et `Articles`.

## 2. Créer les champs calculés

Source **Commandes**. Pour chaque champ : menu **Analysis > Create Calculated Field** (Analyse > Créer un champ calculé), saisir le nom puis la formule, et valider avec **OK**.

| Nom du champ | Formule |
|---|---|
| `Nb commandes` | `COUNTD([commande])` |
| `CA total` | `SUM([chiffre_affaires])` |
| `Panier moyen` | `SUM([chiffre_affaires]) / COUNTD([commande])` |
| `Taux de retard` | `AVG([en_retard])` |
| `Note moyenne` | `AVG([note])` |
| `Part de notes négatives` | `AVG([note_negative])` |
| `Délai moyen (jours)` | `AVG([delai_livraison_jours])` |
| `Taux de clients récurrents` | `COUNTD(IF [client_recurrent] = 1 THEN [client] END) / COUNTD([client])` |

Mise en forme des pourcentages : clic droit sur `Taux de retard`, `Part de notes négatives` et `Taux de clients récurrents` > **Default Properties > Number Format > Percentage**, 1 décimale.

Ordre des tranches de retard : clic droit sur `tranche_retard` > **Default Properties > Sort** > **Manual**, puis ranger dans l'ordre : `À l'heure ou en avance`, `1 à 3 jours`, `4 à 7 jours`, `8 à 14 jours`, `Plus de 14 jours`.

## 3. Construire les feuilles

Créer chaque feuille avec l'icône **New Worksheet** (Nouvelle feuille) en bas de l'écran, puis la renommer (double-clic sur l'onglet).

### Vue 1 — Croissance

| Feuille | Construction |
|---|---|
| `KPI` | Glisser **Measure Names** dans Filtres et ne garder que `Nb commandes`, `CA total`, `Panier moyen`, `Note moyenne`. Glisser **Measure Values** dans Texte, **Measure Names** dans Colonnes. |
| `CA mensuel` | `date_achat` dans Colonnes, puis clic droit sur la pastille > **Month** (format mois-année, la seconde option « Month » en bas de la liste). `CA total` dans Lignes. Type de graphique : **Line**. |
| `Commandes par mois` | Même construction avec `Nb commandes`. |
| `Moyens de paiement` | `moyen_paiement` dans Lignes, `Nb commandes` dans Colonnes, tri décroissant. |

### Vue 2 — Offre et géographie

| Feuille | Construction |
|---|---|
| `Top catégories` | Source **Articles**. `categorie` dans Lignes, `SUM(prix)` dans Colonnes, tri décroissant. Glisser `categorie` dans Filtres > onglet **Top** > **By field**, Top **15** par `prix` (Sum). |
| `Carte des ventes` | Source **Commandes**. Double-clic sur `etat_client` : la carte du Brésil s'affiche. `CA total` sur Couleur, `Nb commandes` sur Info-bulle. Type : **Map** (carte remplie). |
| `Retard par État` | Même carte avec `Taux de retard` sur Couleur (palette Orange). |

### Vue 3 — Livraison, satisfaction et fidélité

| Feuille | Construction |
|---|---|
| `Note selon le retard` | `tranche_retard` dans Colonnes, `Note moyenne` dans Lignes, type **Bar**. Ajouter `Note moyenne` sur Étiquette. |
| `Notes négatives selon le retard` | Même construction avec `Part de notes négatives`. |
| `Indicateurs de service` | Comme la feuille `KPI`, avec `Délai moyen (jours)`, `Taux de retard`, `Taux de clients récurrents`. |

## 4. Assembler les tableaux de bord

Pour chaque vue : icône **New Dashboard** (Nouveau tableau de bord) en bas de l'écran.

1. Volet **Size** (Taille) : **Fixed size**, 1200 × 900.
2. Glisser les feuilles de la vue depuis la liste de gauche.
3. Ajouter un titre : cocher **Show dashboard title** (Afficher le titre du tableau de bord) et saisir le titre de la vue.
4. Filtres communs (vues 1 et 3) : sur la feuille principale, clic droit sur `date_achat` > **Show Filter**, puis dans le filtre affiché, menu de la flèche > **Apply to Worksheets > All Using This Data Source**. Faire de même avec `etat_client`.
5. Filtre par clic sur la carte (vue 2) : menu **Dashboard > Actions > Add Action > Filter**, source `Carte des ventes`, cible toutes les feuilles, exécution **Select**.

Titres proposés :
- Vue 1 : `Croissance de l'activité`
- Vue 2 : `Offre et géographie`
- Vue 3 : `Livraison, satisfaction et fidélité`

## 5. Contrôler les chiffres

Les indicateurs de la feuille `KPI` doivent être identiques à ceux affichés à la fin du notebook (section 8 : nombre de commandes, chiffre d'affaires, panier moyen, note moyenne). Un écart signale un filtre oublié ou un mauvais type de donnée.

## 6. Publier

1. Menu **File > Save to Tableau Public As…** (Fichier > Enregistrer sur Tableau Public sous…).
2. Nom : `Olist - Performance e-commerce`.
3. Le navigateur s'ouvre sur le classeur publié. Copier son adresse : c'est le lien à ajouter dans le README et sur le CV.

À noter : sur Tableau Public, le classeur et ses données sont visibles par tous. Les données Olist étant publiques et anonymisées, cela ne pose pas de difficulté.
