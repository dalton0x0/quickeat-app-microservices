# QuickEat MicroServices API
A basic exercise of microservice APIs without using Eureka, actuator and more ...

## Services

- Booking Service → Auth Service (validation utilisateur)
- Booking Service → Restaurant Service (vérification capacité)
- Review Service → Auth Service (validation utilisateur)
- Review Service → Booking Service (validation réservation terminée)
- Restaurant Service → Auth Service (validation propriétaire)

### En développement

- **auth-service** (8081) - Authentification (en cours)
- **restaurant-service** (8082) - Gestion de la restauration
- **booking-service** (8083) - Gestion des réservations
- **review-service** (8084) - Gestion des historiques et avis

## Technologies

- Backend : Spring Boot 3.2, Spring Cloud 2023
- Database : MySQL 8.0
- Security : Spring Security + JWT
- Frontend : Pas encore implémenté

## Go

```bash
git clone https://github.com/dalton0x0/quickeat-app-microservices.git
```

```bash
cd quickeat-app-microservices
```
---
## Git Workflow - Bonnes Pratiques d’Équipe

Cette partie définit les **règles et conventions Git** à suivre dans ce projet (selon ce que j'ai appris dans mes recherches).  
Il permet de maintenir un code propre, des commits clairs et une collaboration fluide entre développeurs.  

---

## Structure des branches

Nous utilisons une structure de branches inspirée de **Git Flow** (mais nous n'allons pas utilisé les releases) :


| Branche | Rôle |
|----------|------|
| **main** | Code stable en production |
| **develop** | Code d’intégration (pré-production) |
| **feature/** | Nouvelles fonctionnalités |
| **fix/** | Corrections de bugs |
| **hotfix/** | Correctifs urgents en production |
| **release/** | Préparation d’une version stable (que nous allons ignorer pour l'instant) |

---

## Workflow complet

### Très important !!!

Toutes ces commandes git sans à faire dans le dossier racine du projet c'est-à-dire dans votre **terminal** vous trouvez dans le dossier `quickeat-app-microservices/` 
mais pas dans un sous dossier de service. Par exemple si dans votre terminal vous vous trouvez dans le dossier `auth-service/`, **Ce n'est pas le bon emplacement !!!**

----

### 1. Initialisation du dépôt

```bash
git init
```

```bash
git checkout -b main
```

```bash
git pull -u origin main
```

```bash
git checkout -b develop
```

```bash
git pull -u origin develop
```

### 2. Création d'une branche de fonctionnalité

Depuis **develop**

```bash
git checkout -b develop
```

```bash
git pull origin develop
```

```bash
git checkout -b feature/nom-fonctionnalité
```

Exemple :
```bash
git checkout -b feature/ajout-authentification-jwt
```

### 3. Rédiger des commits clairs

Utilisez la convention [Conventional Commits](https://www.conventionalcommits.org/)

```shell
<type>(scope) : message court et clair
```

#### Types courants

| Type | Description |
|------|-------------|
| **feat** | Nouvelle fonctionnalité |
| **fix** | Correction de  bug |
| **docs** | Documentation uniquement |
| **style** | Changement de style, identation, formatage |
| **refactor** | Refactorisation  sans changement de comportement |
| **test** | Ajout/modification de tests |
| **chore** | Maintenance, dépendances, build, etc. |

Exemples :

```bash
git commit -m "feat(auth): ajout de la connexion JWT"
```

```bash
git commit -m "fix(login): correction du bug d’expiration du token"
```

```bash
git commit -m "docs(readme): ajout des instructions d’installation"
```

### 4. Pousser la branche

```bash
git push -u origin feature/ajout-authentification-jwt
```

### 5. Créer une Pull Request (PR)

Sur Github :

- Cliquer sur : `Compare & Pull Request` ou se rendre dans le menu `Pull Request` -> `Create Pull Request`
- **Base** `develop` <- **Compare** `votre-branche`
- Vérifier à bien **choisir** la branche `develop` comme `base` : branche sur laquelle on fera le merge si tout est OK)
- Et de choisir `votre-branche` dans `Compare` : branche pour laquelle on créé la PR

Avant de merger sur **develop**, le code est revu par au moins un autre developpeur et est validé <br>
Ensuite le code sera mergé sur **main** à l'instant ou après avec les fonctionnalités en cours de développement <br>
Enfin il ne faudra pas oublié de supprimer votre branche :

```bash
git branch -d feature/ajout-authentification-jwt
```

Et de récupérer les mises à jour en local des branches **develop** et **main** (si on a déjà mergé main aussi)

```bash
git checkout -b main
```

```bash
git pull origin main
```

```bash
git checkout -b develop
```

```bash
git pull origin develop
```

### 6. Corriger un bug urgent (Hotfix)

```bash
git checkout -b main
```

```bash
git pull origin main
```

```bash
git checkout -b hotfix/bug-urgent
```

Corrige, commit, puis merge vers :

- `main`
- `develop`

### 7. Bonnes pratiques

- Toujours créer les branches à partir de **develop**
- Un commit = une seule intention
- Toujours faire un **pull** avant un merge ou un rebase
- **Supprimer** les branches après merge
- Utiliser un template de PR clair (titre, description, tests)

### 8. Récap

#### Créer une branche
```bash
git checkout -b feature/ajout-avis
```

#### Travailler et commit

- Tout ajouter dans un seul commit :

```bash
git add .
```

```bash
git commit -m "feat(avis): ajout du service de création d’avis"
```

- Plusieurs commit par fichier :

```bash
git add pom.xml
```

```bash
git commit -m "chore(pom): ajout de la dependance swagger"
```

```bash
git add src/main/java/com/quickeat/authservice/entities/User.java
```

```bash
git commit -m "feat(auth): ajout de l'entité user"
```

#### Pousser et créer une PR
```bash
git push origin feature/ajout-avis
```

#### Vérification et validation

`PR -> Review -> Merge -> Supprimer la branche`
