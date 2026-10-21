# Performance d'une place de marché en ligne : croissance, satisfaction et fidélité

> Tableau de bord de pilotage construit sur près de 100 000 commandes réelles de la place de marché brésilienne Olist : évolution de l'activité, catégories et régions qui portent la croissance, effet des retards de livraison sur la satisfaction et fidélité des clients.

**Outils :** Python (pandas) pour la préparation, Tableau Public pour la visualisation

**Dashboard interactif :** [Olist - Performance e-commerce sur Tableau Public](https://public.tableau.com/app/profile/n.c.danielle.ouattara/viz/Olist-Performancee-commerce)

---

## 1. Contexte

Olist permet à de petits commerçants de vendre sur les grands sites de e-commerce brésiliens. L'entreprise a publié les données anonymisées de ses commandes de 2016 à 2018.

L'objectif est de donner à une direction commerciale et marketing un tableau de bord unique pour suivre la croissance, comprendre ce qui dégrade la satisfaction et identifier les leviers de fidélisation.

La note de cadrage est disponible dans [`docs/brief_cadrage.md`](docs/brief_cadrage.md).

## 2. Questions traitées

1. Comment évoluent les commandes et le chiffre d'affaires ?
2. Quelles catégories de produits portent le chiffre d'affaires ?
3. D'où viennent les clients, et la qualité de livraison est-elle la même partout ?
4. Quel est l'effet d'un retard de livraison sur la note laissée par le client ?
5. Quelle part des clients revient acheter une seconde fois ?

## 3. Résultats clés

| Indicateur | Valeur (janvier 2017 à août 2018) |
|---|---|
| Commandes livrées | 96 203 |
| Chiffre d'affaires | 13,18 M R$ |
| Panier moyen | 137 R$ |
| Note moyenne | 4,16 / 5 |
| Délai moyen de livraison | 12,1 jours |
| Taux de retard | 6,8 % |
| Clients ayant commandé au moins deux fois | 3,0 % |

### Croissance

- L'activité a été multipliée par près de 9 en 2017 : environ 110 000 R$ de chiffre d'affaires en janvier, près de 1 M R$ en novembre.
- Novembre 2017 (Black Friday) est le pic de la période, avec environ 7 300 commandes. L'activité se stabilise ensuite autour de 6 000 à 7 000 commandes par mois en 2018.
- La carte de crédit règle 75,5 % des commandes, devant le boleto, bordereau de paiement brésilien (19,9 %).

### Offre et géographie

- Les cinq premières catégories (santé et beauté, montres et cadeaux, linge de maison, sports et loisirs, accessoires informatiques) représentent environ 40 % du chiffre d'affaires.
- L'État de São Paulo concentre 42 % des commandes et 38 % du chiffre d'affaires.
- Le taux de retard varie de 2,8 % à 21,5 % selon l'État. Les États du Nord-Est, éloignés des vendeurs concentrés dans le Sud-Est, sont les plus touchés (Bahia : 12,2 %, près du double de la moyenne).

### Livraison et satisfaction

| Retard de livraison | Note moyenne | Part de notes de 1 ou 2 sur 5 |
|---|---|---|
| À l'heure ou en avance | 4,29 | 9,2 % |
| 1 à 3 jours | 3,29 | 31,8 % |
| 4 à 7 jours | 2,10 | 65,6 % |
| 8 à 14 jours | 1,67 | 78,4 % |
| Plus de 14 jours | 1,72 | 75,5 % |

Un seul à trois jours de retard fait perdre un point de note et multiplie par trois la part d'avis négatifs. Au-delà d'une semaine, près de 8 clients sur 10 laissent une mauvaise note.

### Fidélité

Seuls 3 % des clients ont passé une seconde commande sur la période. La croissance repose presque entièrement sur l'acquisition de nouveaux clients.

## 4. Recommandations

1. **Fiabiliser la promesse de livraison avant tout.** Le retard est le premier facteur de mécontentement mesuré. Deux leviers : allonger la date estimée pour les destinations lointaines plutôt que promettre un délai intenable, et prévenir le client dès qu'un retard est détecté.
2. **Traiter le Nord-Est comme une zone prioritaire.** Un partenaire logistique régional ou des vendeurs implantés localement réduiraient les retards là où ils sont les plus fréquents, et ouvriraient un relais de croissance hors de São Paulo.
3. **Lancer un programme de réachat.** Avec 3 % de clients récurrents, une hausse même modeste du réachat (offre après une première livraison réussie, relance sur les catégories à achat répété comme la santé et la beauté) aurait un effet direct sur le chiffre d'affaires.
4. **Préparer les pics commerciaux.** Le Black Friday double presque l'activité d'un mois normal : anticiper les capacités de livraison sur cette période évite de dégrader la note au moment où le plus de nouveaux clients découvrent la plateforme.

## 5. Données

| Élément | Détail |
|---|---|
| Jeu de données | *Brazilian E-Commerce Public Dataset by Olist* — Kaggle |
| Lien | https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce |
| Tables | 9 tables : commandes, clients, articles, paiements, avis, produits, vendeurs, géolocalisation, traduction des catégories |
| Période analysée | Janvier 2017 à août 2018 (mois complets), commandes livrées |
| Devise | Réal brésilien (R$) |
| Licence | CC BY-NC-SA 4.0 (attribution, usage non commercial, partage dans les mêmes conditions) |

Les données ne sont pas incluses dans ce dépôt. Pour reproduire l'analyse, téléchargez les fichiers sur Kaggle et placez-les dans le dossier `data/`.

## 6. Méthode

| Étape | Ce qui est fait | Fichier |
|---|---|---|
| Préparation | Jointure des 9 tables, périmètre (commandes livrées, mois complets), calcul des délais et des retards, catégorie principale de chaque commande, identification des clients récurrents | `notebooks/01_preparation_tableau.ipynb` |
| Visualisation | Trois tableaux de bord : croissance de l'activité ; offre et géographie ; livraison, satisfaction et fidélité | `tableau/guide_tableau.md` |

Les indicateurs affichés dans Tableau ont été contrôlés par rapport aux valeurs calculées dans le notebook.

## 7. Limites

- Les données datent de 2017-2018 et concernent le Brésil : le projet illustre une démarche de pilotage, pas un marché actuel.
- Le lien entre retard et note est une corrélation : d'autres facteurs (qualité du produit, vendeur) peuvent jouer, mais l'écart observé est trop important pour être fortuit.
- Le chiffre d'affaires est celui des commerçants vendus via Olist, pas le revenu propre d'Olist, dont les commissions ne sont pas publiées.
- Le classement des catégories porte sur l'ensemble de la période et n'est pas filtré par État.

## 8. Structure du dépôt

```
olist-ecommerce-performance-dashboard/
├── README.md
├── requirements.txt
├── docs/
│   └── brief_cadrage.md               note de cadrage du projet
├── data/                              fichiers Olist à télécharger (non versionnés)
├── notebooks/
│   └── 01_preparation_tableau.ipynb   préparation des données
├── outputs/                           fichiers générés pour Tableau (non versionnés)
└── tableau/
    └── guide_tableau.md               construction du dashboard pas à pas
```

## 9. Reproduire l'analyse

```bash
git clone https://github.com/niyadanielleO/olist-ecommerce-performance-dashboard.git
cd olist-ecommerce-performance-dashboard
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
mkdir -p data outputs
jupyter notebook
```

Placer les fichiers Olist dans `data/`, exécuter le notebook, puis suivre `tableau/guide_tableau.md`.

---

**N. Danielle OUATTARA** · [LinkedIn](https://www.linkedin.com/in/ndanielleouattara/) · [Mes autres projets](https://github.com/niyadanielleO)
