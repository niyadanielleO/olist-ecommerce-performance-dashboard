# Note de cadrage — Tableau de bord de performance d'une place de marché en ligne

**Projet :** Pilotage de la performance e-commerce d'Olist
**Auteure :** Niya C. Danielle Ouattara
**Version :** 1.0 — octobre 2026

---

## 1. Contexte

Olist est une place de marché brésilienne : elle permet à de petits commerçants de vendre sur les grands sites de e-commerce du pays. Elle a publié les données anonymisées d'environ 100 000 commandes passées entre 2016 et 2018 : clients, articles, paiements, livraisons et avis.

La direction commerciale et marketing souhaite disposer d'un tableau de bord unique pour suivre la croissance, comprendre ce qui dégrade la satisfaction client et identifier les leviers de fidélisation.

## 2. Questions posées

1. **Croissance** : comment évoluent les commandes et le chiffre d'affaires ? Y a-t-il une saisonnalité ?
2. **Offre** : quelles catégories de produits portent le chiffre d'affaires ?
3. **Géographie** : d'où viennent les clients, et la qualité de livraison est-elle la même partout ?
4. **Satisfaction** : quel est l'effet d'un retard de livraison sur la note laissée par le client ?
5. **Fidélité** : quelle part des clients revient acheter une seconde fois ?

## 3. Périmètre et données

| Élément | Détail |
|---|---|
| Source | *Brazilian E-Commerce Public Dataset by Olist* — Kaggle |
| Lien | https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce |
| Volume | Environ 100 000 commandes, 9 tables reliées par des identifiants |
| Période | Septembre 2016 à octobre 2018 |
| Devise | Réal brésilien (R$) |
| Périmètre retenu | Commandes livrées, sur les mois où l'activité est complète |

## 4. Indicateurs suivis

| Indicateur | Définition |
|---|---|
| Chiffre d'affaires | Somme des prix des articles, hors frais de port |
| Panier moyen | Chiffre d'affaires / nombre de commandes |
| Délai de livraison | Jours entre l'achat et la livraison |
| Taux de retard | Part des commandes livrées après la date estimée |
| Note moyenne | Moyenne des avis clients (de 1 à 5) |
| Taux de clients récurrents | Part des clients ayant passé au moins deux commandes |

## 5. Démarche

| Étape | Livrable |
|---|---|
| Préparation des données | Deux tables prêtes pour Tableau — notebook `01_preparation_tableau` |
| Construction du tableau de bord | Trois vues dans Tableau Public — guide `tableau/guide_tableau.md` |
| Restitution | Constats et recommandations dans le README |

## 6. Limites connues

- Les données datent de 2016 à 2018 et concernent le Brésil : le projet illustre une démarche de pilotage, pas un marché actuel.
- Le jeu de données a été anonymisé par Olist ; certains champs (noms des produits, identité des vendeurs) ne sont pas disponibles.
- Le chiffre d'affaires est celui des commerçants vendus via Olist, pas le revenu propre d'Olist (ses commissions ne sont pas publiées).
