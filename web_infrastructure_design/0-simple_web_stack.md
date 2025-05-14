""# Infrastructure Web à Serveur Unique

## 🎯 Objectif : Concevoir une infrastructure web simple qui héberge le site [www.foobar.com](http://www.foobar.com) sur un seul serveur.

---

## 📌 1️⃣ Description du scénario

Un utilisateur veut accéder à l'adresse **[www.foobar.com](http://www.foobar.com)** depuis son navigateur.

### Étapes :

1. L'utilisateur entre l'URL **[www.foobar.com](http://www.foobar.com)** dans son navigateur.
2. Une requête DNS est envoyée pour résoudre le nom de domaine.
3. Le DNS renvoie l'adresse IP associée : **8.8.8.8**.
4. Le navigateur envoie une requête HTTP/HTTPS à l'adresse **8.8.8.8**.
5. Le serveur (à cette adresse) reçoit la requête, la traite et envoie le contenu de la page web en réponse.

---

## 📌 2️⃣ Architecture du serveur

L'infrastructure est composée d'un unique serveur qui regroupe :

* **Web Server (Nginx)** : Sert les fichiers statiques (HTML, CSS, JS) et gère les requêtes HTTP.
* **Application Server** : Exécute le code backend (PHP, Node.js, Python, etc.).
* **Fichiers de l'application** : Le code source de l'application.
* **Base de données (MySQL)** : Stocke les données nécessaires au fonctionnement du site.

---

## 📌 3️⃣ Explication des composants

| Composant                   | Rôle                                                                                |
| --------------------------- | ----------------------------------------------------------------------------------- |
| **Serveur**                 | Machine physique ou virtuelle qui héberge le site web.                              |
| **Nom de domaine**          | Adresse lisible par l'humain (foobar.com) qui pointe vers l'IP.                     |
| **DNS Record (www)**        | Type **A** qui lie le nom de domaine à l'IP (8.8.8.8).                              |
| **Web Server (Nginx)**      | Gère les requêtes HTTP et sert les fichiers statiques.                              |
| **Application Server**      | Exécute la logique backend (traitement des données, authentification, etc.).        |
| **Base de données (MySQL)** | Stocke les informations (utilisateurs, articles, etc.).                             |
| **Communication**           | Se fait via les protocoles **HTTP** ou **HTTPS** entre le serveur et l'utilisateur. |

---

## 📌 4️⃣ Problèmes identifiés

1. **Single Point Of Failure (SPOF)** :
   Si le serveur tombe en panne, tout le site devient inaccessible.

2. **Downtime pendant la maintenance** :
   Lors d'une mise à jour, le serveur doit redémarrer, ce qui cause une indisponibilité temporaire.

3. **Manque de scalabilité** :
   Le serveur unique ne peut pas supporter un trafic massif. En cas de surcharge, le site devient lent ou inaccessible.

---

## 📌 5️⃣ Diagramme d'infrastructure

Un schéma va être fourni pour illustrer cette architecture.

```mermaid
graph TD
    A[Utilisateur] -->|Requête HTTP/HTTPS| B[Serveur]
    B --> C[Web Server (Nginx)]
    C --> D[Application Server]
    D --> E[Base de données (MySQL)]
```
