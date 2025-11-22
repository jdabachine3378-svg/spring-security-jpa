# 🌐 Spring Security JPA — Authentication avec Base de Données

## 📌 Introduction
Dans les TP précédents, l’authentification se faisait en mémoire via `InMemoryUserDetailsManager`.  
Cette méthode est utile pour les tests, mais **les données disparaissent à chaque redémarrage**.

Dans ce projet, nous mettons en place **une authentification réelle et persistante**, basée sur :
- une base de données MySQL,
- JPA pour gérer les entités (User, Role),
- Spring Security pour protéger les pages,
- un service personnalisé `UserDetailsService` pour charger les utilisateurs.

L’objectif est de comprendre comment Spring Security fonctionne avec une base de données relationnelle.

---

## 🎯 Objectifs du projet
- Mettre en place un système d’authentification sécurisé.
- Stocker les utilisateurs et rôles dans MySQL.
- Configurer Spring Security avec JPA.
- Créer un formulaire de connexion personnalisé via Thymeleaf.
- Restreindre l’accès aux pages selon les rôles :  
  - `ADMIN` → accès aux pages admin  
  - `USER` → accès aux pages user  
  - Tous les utilisateurs → accès à /login  
- Initialiser la base avec des utilisateurs par défaut.
- Effectuer des tests fonctionnels de l’authentification.

---

## 🛠️ Outils & Technologies Utilisés

| Outil / Technologie | Rôle |
|---------------------|------|
| **Java 17+** | Langage backend |
| **Spring Boot 3.x** | Framework principal |
| **Spring Security** | Authentification & autorisation |
| **Spring Data JPA** | Mapping Objet–Relation |
| **MySQL** | Base de données |
| **Thymeleaf** | Front-end HTML |
| **Lombok** | Réduction du code boilerplate |
| **Maven** | Gestion des dépendances |
| **IntelliJ IDEA** | IDE de développement |

---


---

## 📁 Structure du projet (arborescence)
<img width="650" height="804" alt="image" src="https://github.com/user-attachments/assets/d402ea3b-0bb8-41cd-8708-43b1579ddfaa" />


## 🔐 Fonctionnement global de l’authentification

L’utilisateur accède à /login.

Il saisit username + password.

Spring Security utilise CustomUserDetailsService pour :

vérifier si l’utilisateur existe

récupérer son mot de passe hashé

récupérer ses rôles

BCrypt compare les mots de passe.

Si OK → redirection vers /home.

Si KO → redirection vers /login?error=true.

Les pages “admin” et “users” sont filtrées en fonction des rôles.

## 🗄️ Base de données (MySQL)
Tables générées automatiquement :

user

role

user_roles (ManyToMany)

## Utilisateurs initialisés
username	password	roles
admin	1234	ADMIN + USER
user	1111	USER

(Pass hashés avec BCrypt)

## 🧪 Tests fonctionnels
## ✔ Test 1 — Page de login

URL : http://localhost:8085/login

Résultat : formulaire s’affiche

## ✔ Test 2 — Login correct (admin)

username : admin

password : 1234

Résultat : accès autorisé à /home

## ✔ Test 3 — Login incorrect

username : admin

password : 0000

Résultat : /login?error=true

## ✔ Test 4 — Accès non authentifié

Aller à /home sans login

Résultat : redirection automatique → /login

## ✔ Test 5 — Rôles (si routes Admin/User existent)

USER ne peut pas entrer dans ADMIN

ADMIN peut accéder à tout


https://github.com/user-attachments/assets/a40a84ec-aa60-4f9f-b16c-c48c41fc8cce





## 🧾 Conclusion

Ce projet montre comment :

intégrer Spring Security avec JPA/MySQL,

gérer les utilisateurs et rôles,

sécuriser une application web moderne avec BCrypt,

comprendre le flux d’authentification complet,

mettre en place un login personnalisé via Thymeleaf.

Ce TP constitue une base solide pour développer :

un système d'inscription,

un panneau d’administration,

OAuth2 (Google, GitHub),

JWT et microservices.
