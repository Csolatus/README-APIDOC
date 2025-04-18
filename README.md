<div align="center"> <img src="public/zizou.webp" width=250px> </div>

# 🍽️ Application de Gestion de Restaurant

## 🧾 Description

Cette application **Java** permet de gérer l'ensemble des opérations d'un **restaurant**, depuis la création de **menus** jusqu'à la gestion des **commandes**, des **stocks** et du **personnel**. Elle utilise une base de données **MySQL** pour stocker toutes les informations et offre une **interface en ligne de commande** pour interagir avec le système.

## ✅ Fonctionnalités

L'application propose les **fonctionnalités suivantes** :

| Module              | Fonctionnalités principales                                                                 |
|---------------------|---------------------------------------------------------------------------------------------|
| **Menu**            | - Créer / afficher / supprimer des **plats**<br>- Gérer les **ingrédients** de chaque **plat**         |
| **Stock**           | - Initialiser / afficher / ajouter des **ingrédients**<br>- Mise à jour **automatique** avec commandes |
| **Commandes**       | - Créer / afficher / mettre à jour les **commandes**<br>- Calcul automatique du **total**           |
| **Employés**        | - Ajouter / afficher / supprimer des **employés**<br>- Gérer les **rôles** (Serveur, Cuisinier, Gérant) |

---

## 🧱 Architecture du Système

L'application est structurée selon le modèle **orienté objet** avec les principales classes suivantes :

| Classe         | Description                                                              |
|----------------|--------------------------------------------------------------------------|
| `Plat`         | Représente un **plat** (nom, prix, type, liste d’ingrédients)               |
| `Ingredient`   | Nom, quantité, unité de mesure                                           |
| `Menu`         | Liste de **plats** disponibles                                               |
| `Stock`        | Gestion des **ingrédients** en stock                                         |
| `Commande`     | Contient les **plats** commandés                                             |
| `Employe`      | Classe abstraite : `Serveur`, `Cuisinier`, `Gerant`                      |
| `Database`     | Gère les **connexions et requêtes** vers **MySQL** via **JDBC**                     |

---

### 🗃️ Base de données

| Table                | Rôle                                                                 |
|----------------------|----------------------------------------------------------------------|
| `ingredients`        | **Ingrédients** disponibles                                              |
| `plats`              | **Plats** proposés dans le **menu**                                          |
| `plats_ingredients`  | Liaison entre **plats** et **ingrédients**                                   |
| `commandes`          | Informations sur les **commandes**                                       |
| `commandes_plats`    | Liaison entre **commandes** et **plats**                                     |
| `employes`           | Informations sur les **employés**                                        |

---
## ⚙️ Prérequis

| Logiciel    | Version recommandée | Lien de téléchargement                                        |
|-------------|---------------------|----------------------------------------------------------------|
| **Java JDK**| 8 ou supérieur       | [Télécharger Java](https://www.oracle.com/java/technologies/javase-downloads.html) |
| **MySQL**   | 5.7 ou supérieur    | [Télécharger MySQL](https://dev.mysql.com/downloads/mysql/)   |
| **JDBC Driver** | MySQL Connector/J | [Télécharger le Connecteur JDBC](https://dev.mysql.com/downloads/connector/j/) |

> [!WARNING]
> Assurez-vous que **MySQL est installé**, **en cours d'exécution** et que **le port 3306** est bien ouvert.

---

### 🖥️ Installation rapide en ligne de commande (Linux/Debian/Ubuntu)

#### Installer Java (OpenJDK 11 recommandé)

```bash
sudo apt update
sudo apt install openjdk-11-jdk
java -version
```

### Installer MySQL Server

```bash
sudo apt install mysql-server
sudo systemctl start mysql
sudo systemctl enable mysql
mysql --version
```

### (Optionnel) Sécuriser MySQL

```bash
sudo mysql_secure_installation
```  

### Télécharger et ajouter le JDBC Driver (manuel)

1. Télécharger le .jar depuis : https://dev.mysql.com/downloads/connector/j/
2. Ajouter le fichier .jar dans le classpath lors de la compilation ou l'exécution :
   
```bash
javac -cp .:mysql-connector-j-8.4.0.jar Main.java
java -cp .:mysql-connector-j-8.4.0.jar Main
```

## 🛠️ Installation

1. **Clonez** ce dépôt sur votre machine locale
   
```bash
git clone https://github.com/ton-utilisateur/restaurant-manager.git
cd restaurant-manager
```

2. **Créez** la base de données **MySQL**

```sql
-- Depuis le terminal MySQL :
CREATE DATABASE restaurant;
```

> [!NOTE] La base de données peut aussi être créée automatiquement au lancement de l'application.

3. **Configurez** la connexion dans **Database.java**
**Modifiez** les constantes suivantes avec vos **identifiants MySQL** :
```java
public static final String DB_URL = "jdbc:mysql://localhost:3306/restaurant";
public static final String DB_USER = "root";
public static final String DB_PASSWORD = "votre_mot_de_passe";
```

4. **Compilez** et **lancez** le projet:
```bash
javac -cp .:mysql-connector-j-8.4.0.jar Main.java
java -cp .:mysql-connector-j-8.4.0.jar Main
```
## ▶️ Utilisation

1. Lancez l'**application** via la classe `Main`
2. Utilisez le **menu interactif** pour accéder aux différentes **fonctionnalités**
3. Suivez les **instructions** affichées à l'écran

## 💡 Exemples d'Utilisation

### ➕ Créer un Menu
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

### 🧾 Créer une Commande
```java
Commande commande = new Commande("Commande client", 0, "Commande");
commande.ajouterPlat(pizza);
Database.sauvegarderCommande(commande);
```

## 🌐 API RESTful

L’application expose une API RESTful documentée avec Swagger.

## 🔗 Base Url 

http://LaBellaTravola

## 🚀 Améliorations Futures

- Interface graphique utilisateur (GUI)
- Authentification et gestion des rôles
- Statistiques et reporting
- Gestion des réservations de tables
- Système de fidélité clients

## 📄 Licence

Ce projet est sous **licence MIT**.

[![Anurag's GitHub stats](https://github-readme-stats.vercel.app/api?username=Csolatus)](https://github.com/anuraghazra/github-readme-stats)
