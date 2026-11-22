# 🎓 ProjectIQ — Academic Project Intelligence

<div align="center">

![.NET](https://img.shields.io/badge/.NET-8.0-512BD4?style=for-the-badge&logo=dotnet&logoColor=white)
![Blazor](https://img.shields.io/badge/Blazor-Server-512BD4?style=for-the-badge&logo=blazor&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=for-the-badge&logo=sqlite&logoColor=white)
![EF Core](https://img.shields.io/badge/EF_Core-8.0-512BD4?style=for-the-badge&logo=dotnet&logoColor=white)
![Bootstrap](https://img.shields.io/badge/Bootstrap-5.3-7952B3?style=for-the-badge&logo=bootstrap&logoColor=white)

**Application web de gestion de projets académiques avec indicateurs de performance**

*Mini-Projet — Sujet 5 | Encadrant : Said Sassi*

[Fonctionnalités](#-fonctionnalités) •
[Installation](#-installation) •
[Architecture](#-architecture) •
[Indicateurs](#-indicateurs) •
[Comptes demo](#-comptes-de-démonstration)

</div>

---

## 📋 Présentation

**ProjectIQ** est une application web complète développée avec **Blazor Server** et **Entity Framework Core** permettant la gestion de projets académiques avec un tableau de bord analytique avancé.

L'application implémente une **architecture en couches** (UI / Services / Data), une **authentification utilisateur** complète, et un système d'**indicateurs de performance** calculés automatiquement pour chaque projet et chaque membre de l'équipe.

### ✨ Points forts

- 🌙 **Interface dark moderne** — Design glassmorphism avec la police Inter
- 🔐 **Authentification complète** — Login, Register, Profil utilisateur
- 📊 **Tableau de bord analytique** — Graphiques Chart.js interactifs
- ⚡ **Détection automatique des retards** — BackgroundService toutes les heures
- 🗄️ **Zéro configuration** — SQLite, base de données créée au démarrage

---

## 🚀 Fonctionnalités

### Gestion des projets
- ✅ CRUD complet (Créer, Lire, Modifier, Supprimer)
- ✅ Recherche textuelle et filtrage par statut
- ✅ Health Score calculé en temps réel
- ✅ Indicateur de jours restants / dépassement

### Gestion des tâches
- ✅ CRUD complet avec priorité et échéance
- ✅ Assignation de membres aux tâches
- ✅ Détection automatique des retards (règle métier + BackgroundService)
- ✅ Filtrage multi-critères (projet, statut, priorité)

### Gestion des membres
- ✅ CRUD complet avec validation email unique
- ✅ Cartes membres avec indicateurs de charge
- ✅ Taux de complétion par membre

### Authentification & Profil
- ✅ Page de connexion avec comptes de démonstration
- ✅ Page d'inscription avec sélecteur de rôle visuel
- ✅ Page profil : modification des informations personnelles
- ✅ Changement de mot de passe sécurisé (SHA-256 + salt)
- ✅ Session Blazor Server par circuit (`AuthStateService`)

### Tableau de bord & Indicateurs
- ✅ 4 KPI cards animées
- ✅ Graphique camembert (répartition des tâches)
- ✅ Graphique à barres (Health Score par projet)
- ✅ Table d'alertes pour les projets en retard
- ✅ Classement des membres par performance
- ✅ Page indicateurs dédiée (onglets Projets / Membres)

---

## 🛠️ Installation

### Prérequis

- [.NET 8 SDK](https://dotnet.microsoft.com/download/dotnet/8) — vérifier avec `dotnet --version`
- Visual Studio 2022 **ou** VS Code + extension C# Dev Kit

### Étapes

```bash
# 1. Cloner le dépôt
git clone https://github.com/takwa-haj/ProjectIntelligence.git
cd ProjectIntelligence

# 2. Aller dans le projet Web
cd ProjectIntelligence.Web

# 3. Restaurer les packages NuGet
dotnet restore

# 4. Lancer l'application
dotnet run
```

> 💡 La base de données SQLite est créée **automatiquement** au premier lancement avec les données de démonstration. Aucune configuration supplémentaire requise.

### Ouvrir dans le navigateur

```
http://localhost:5050
```

### Avec hot-reload (développement)

```bash
dotnet watch run
```

---

## 🔑 Comptes de démonstration

| Rôle | Email | Mot de passe |
|------|-------|-------------|
| 🛡️ Admin | `admin@pi.tn` | `Admin123!` |
| 👔 Chef de Projet | `ahmed@pi.tn` | `User123!` |
| 💻 Développeur | `sara@pi.tn` | `User123!` |
| 🧪 Testeur | `karim@pi.tn` | `User123!` |

> Ces comptes sont disponibles via les boutons de démonstration sur la page de connexion.

---

## 🏗️ Architecture

```
ProjectIntelligence/
├── 📦 ProjectIntelligence.Data/          ← Couche Données
│   ├── Entities/
│   │   └── Entities.cs                   # AppUser, Projet, Tache, Membre, Affectation + Enums
│   ├── Repositories/
│   │   └── Repositories.cs               # Interfaces + Implémentations EF Core
│   └── AppDbContext.cs                   # DbContext + Fluent API + Seed data
│
├── 📦 ProjectIntelligence.Services/      ← Couche Logique Métier
│   ├── DTOs/
│   │   └── DTOs.cs                       # ProjetDto, TacheDto, IndicateurDto, LoginDto...
│   └── Implementations/
│       └── Services.cs                   # AuthService, ProjetService, TacheService,
│                                         # MembreService, AnalytiqueService,
│                                         # RetardBackgroundService
│
└── 📦 ProjectIntelligence.Web/           ← Couche UI (Blazor Server)
    ├── Pages/
    │   ├── Auth/
    │   │   ├── Login.razor               # Page de connexion
    │   │   └── Register.razor            # Page d'inscription
    │   ├── Index.razor                   # Tableau de bord
    │   ├── Projets.razor                 # Liste des projets
    │   ├── ProjetForm.razor              # Formulaire création/modification
    │   ├── Taches.razor                  # Gestion des tâches
    │   ├── Membres.razor                 # Gestion des membres
    │   ├── Indicateurs.razor             # Page indicateurs analytiques
    │   └── Profil.razor                  # Profil utilisateur
    ├── Shared/
    │   └── MainLayout.razor              # Layout (sidebar + topbar)
    ├── Services/
    │   └── AuthStateService.cs           # État d'authentification (Scoped)
    ├── _Imports.razor                    # @using globaux
    ├── Program.cs                        # DI + SQLite + Pipeline
    └── wwwroot/css/app.css               # Design system complet (600+ lignes)
```

### Séparation des responsabilités

| Couche | Technologie | Rôle |
|--------|-------------|------|
| **UI** | Blazor Server | Pages Razor, composants interactifs, binding |
| **Services** | C# / Interfaces | Logique métier, calculs, règles de détection |
| **Data** | EF Core + SQLite | DbContext, repositories, migrations, seed |

---

## 📊 Indicateurs

### Health Score (Projet)

```
HealthScore = (NbTerminées / NbTotal × 100) − (NbRetards × 5)
```

| Score | Catégorie | Couleur |
|-------|-----------|---------|
| ≥ 75 | 🟢 Bon | Vert |
| 50 – 74 | 🟡 Moyen | Orange |
| < 50 | 🔴 Critique | Rouge |

### Score Performance (Membre)

```
ScorePerformance = TauxCompletion − (NbRetards × 3)
```

| Score | Performance |
|-------|------------|
| ≥ 75 | 🟢 Excellent |
| 50 – 74 | 🟡 Moyen |
| < 50 | 🔴 Faible |

### Détection automatique des retards

Une tâche est en retard si :
```csharp
Statut != StatutTache.Terminee && DateEcheance < DateTime.Now
```

Le `RetardBackgroundService` scanne toutes les tâches **toutes les heures** et met à jour leur statut automatiquement.

---

## 🧰 Stack technique

| Technologie | Version | Usage |
|-------------|---------|-------|
| .NET / ASP.NET Core | 8.0 | Framework principal |
| Blazor Server | 8.0 | Interface utilisateur réactive |
| Entity Framework Core | 8.0 | ORM Code-First |
| SQLite | — | Base de données (zéro configuration) |
| Chart.js | 4.4 | Graphiques interactifs (via JSInterop) |
| Bootstrap | 5.3 | Framework CSS responsive |
| Bootstrap Icons | 1.11 | Icônes SVG |
| Inter (Google Fonts) | — | Typographie |
| Blazored.Toast | 4.2 | Notifications |
| Blazored.Modal | 7.3 | Modales |

---

## 🔒 Sécurité

- Mots de passe hashés avec **SHA-256 + salt** côté serveur
- **Validation côté serveur** sur toutes les routes (guards Blazor)
- Contrainte d'unicité sur les emails (niveau BDD)
- `AuthStateService` Scoped — isolation par circuit Blazor

---

## 📐 Barème du projet (20/20)

| Critère | Points | Couvert |
|---------|--------|---------|
| Évaluation collective | 14 pts | ✅ CRUD, architecture, EF Core, LINQ, async |
| Évaluation individuelle | 4 pts | ✅ Chaque membre possède son rôle clair |
| Créativité | 2 pts | ✅ Auth complète + dark theme + profile utilisateur |

---

## 👥 Équipe

> Projet réalisé par une équipe de 2–3 étudiants dans le cadre du
> mini-projet académique **Sujet 5**, encadré par **Said Sassi**.

---

<div align="center">

**ProjectIQ** — Academic Project Intelligence • 2024/2025

Made with ❤️ using Blazor Server & .NET 8

</div>