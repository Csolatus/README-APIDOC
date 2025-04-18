<div> <img src="public/zizou.webp" width=250px> </div>

# Application de Gestion de Restaurant

## Description

Cette application Java permet de gérer l'ensemble des opérations d'un restaurant, depuis la création de menus jusqu'à la gestion des commandes, des stocks et du personnel. Elle utilise une base de données MySQL pour stocker toutes les informations et offre une interface en ligne de commande pour interagir avec le système.

## Fonctionnalités

L'application propose les fonctionnalités suivantes :

| Module              | Fonctionnalités principales                                                                 |
|---------------------|---------------------------------------------------------------------------------------------|
| **Menu**            | - Créer / afficher / supprimer des plats<br>- Gérer les ingrédients de chaque plat         |
| **Stock**           | - Initialiser / afficher / ajouter des ingrédients<br>- Mise à jour automatique avec commandes |
| **Commandes**       | - Créer / afficher / mettre à jour les commandes<br>- Calcul automatique du total           |
| **Employés**        | - Ajouter / afficher / supprimer des employés<br>- Gérer les rôles (Serveur, Cuisinier, Gérant) |

---

## Architecture du Système

L'application est structurée selon le modèle orienté objet avec les principales classes suivantes :

| Classe         | Description                                                              |
|----------------|--------------------------------------------------------------------------|
| `Plat`         | Représente un plat (nom, prix, type, liste d’ingrédients)               |
| `Ingredient`   | Nom, quantité, unité de mesure                                           |
| `Menu`         | Liste de plats disponibles                                               |
| `Stock`        | Gestion des ingrédients en stock                                         |
| `Commande`     | Contient les plats commandés                                             |
| `Employe`      | Classe abstraite : `Serveur`, `Cuisinier`, `Gerant`                      |
| `Database`     | Gère les connexions et requêtes vers MySQL via JDBC                     |

---

### Base de données

| Table                | Rôle                                                                 |
|----------------------|----------------------------------------------------------------------|
| `ingredients`        | Ingrédients disponibles                                              |
| `plats`              | Plats proposés dans le menu                                          |
| `plats_ingredients`  | Liaison entre plats et ingrédients                                   |
| `commandes`          | Informations sur les commandes                                       |
| `commandes_plats`    | Liaison entre commandes et plats                                     |
| `employes`           | Informations sur les employés                                        |

---
## Prérequis

- Java 8 ou supérieur 
- MySQL 5.7 ou supérieur
- Connecteur JDBC pour MySQL

## Installation

1. Clonez ce dépôt sur votre machine locale
2. Assurez-vous que MySQL est installé et en cours d'exécution
3. Créez une base de données nommée `restaurant` (l'application peut le faire automatiquement)
4. Modifiez les constantes de connexion dans la classe `Database.java` si nécessaire :
   - `DB_USER`
   - `DB_PASSWORD`
   - `DB_URL`
5. Compilez le projet

## Utilisation

1. Lancez l'application via la classe `Main`
2. Utilisez le menu interactif pour accéder aux différentes fonctionnalités
3. Suivez les instructions affichées à l'écran

## Exemples d'Utilisation

### Créer un Menu
```java
Menu menu = new Menu("Menu du restaurant", 0, "Menu");

Ingredient farine = new Ingredient("Farine", 1.0, "kg");
Ingredient eau = new Ingredient("Eau", 1.0, "l");
Ingredient fromage = new Ingredient("Fromage", 1.0, "kg");

Plat pizza = new Plat("Pizza Margherita", 10.0, "Pizza");
pizza.ajouterIngredient(farine, 0.2);
pizza.ajouterIngredient(eau, 0.1);
pizza.ajouterIngredient(fromage, 0.15);

menu.ajouterPlat(pizza);

Database.sauvegarderMenu(menu);
```

### Créer une Commande
```java
Commande commande = new Commande("Commande client", 0, "Commande");
commande.ajouterPlat(pizza);
Database.sauvegarderCommande(commande);
```

## API RESTful

Une API RESTful peut être implémentée pour exposer les fonctionnalités de cette application. Voici les endpoints principaux qui pourraient être créés :

### Menu
- `GET /api/menu` - Récupérer tout le menu
- `GET /api/menu/{id}` - Récupérer un plat spécifique
- `POST /api/menu` - Ajouter un plat au menu
- `PUT /api/menu/{id}` - Mettre à jour un plat
- `DELETE /api/menu/{id}` - Supprimer un plat

### Stock
- `GET /api/stock` - Récupérer l'état du stock
- `POST /api/stock` - Ajouter des ingrédients au stock
- `PUT /api/stock/{id}` - Mettre à jour la quantité d'un ingrédient

### Commandes
- `GET /api/commandes` - Récupérer toutes les commandes
- `GET /api/commandes/{id}` - Récupérer une commande spécifique
- `POST /api/commandes` - Créer une nouvelle commande
- `PUT /api/commandes/{id}/status` - Mettre à jour le statut d'une commande

### Employés
- `GET /api/employes` - Récupérer tous les employés
- `GET /api/employes/{id}` - Récupérer un employé spécifique
- `POST /api/employes` - Ajouter un nouvel employé
- `PUT /api/employes/{id}` - Mettre à jour les informations d'un employé
- `DELETE /api/employes/{id}` - Supprimer un employé

## Améliorations Futures

- Interface graphique utilisateur (GUI)
- Authentification et gestion des rôles
- Statistiques et reporting
- Gestion des réservations de tables
- Système de fidélité clients

## Licence

Ce projet est sous licence MIT. Voir le fichier LICENSE pour plus de détails. 
