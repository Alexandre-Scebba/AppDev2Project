# ExAMina

> **ExAMina** est un système de gestion d’examens en ligne construit avec ASP.NET Core MVC pour permettre aux enseignants de créer, attribuer et corriger des examens, et aux étudiants de les passer et de les consulter, sur n’importe quel appareil.

---

## 📝 Présentation du Projet

ExAMina est une application full-stack en C# ASP.NET conçue pour que les enseignants et les étudiants gèrent, distribuent et réalisent des examens en ligne. Les fonctionnalités principales incluent :

* **Création d’examens** : questions QCM, vrai/faux et réponses courtes.
* **Attribution rapide** : distribuez un examen à des classes ou à des étudiants individuels.
* **Suivi et notation** : visualisez l’avancement des étudiants et corrigez en ligne.
* **Interface réactive** : Tailwind CSS + Razor/MVC pour un rendu ergonomique et adapté aux mobiles.
* **Intégration Cloud** : Azure SQL Database pour les données des examens et Azure Blob Storage pour les photos de profil.
* **Notifications** : mises à jour en temps réel et notifications par e-mail (en cours de développement).

---

## 🚀 Fonctionnalités Clés

### Pour les Enseignants

1. **Création de différents types de questions**

   * Support des questions à choix multiple, vrai/faux et réponses courtes.
2. **Attribution des examens aux groupes d’étudiants**

   * Choisissez des classes ou des étudiants individuels pour l’attribution.
3. **Suivi des progrès des étudiants**

   * Surveillez qui a commencé, est en cours ou a terminé un examen.
4. **Notation et retour d’information**

   * Saisissez les notes, laissez des commentaires et publiez les résultats.

### Pour les Étudiants

1. **Consultation des examens en attente et terminés**

   * Le tableau de bord liste les examens disponibles ou déjà soumis.
2. **Passage des examens sur n’importe quel appareil**

   * L’interface réactive s’adapte aux ordinateurs de bureau et aux mobiles.
3. **Édition des réponses jusqu’à la soumission**

   * Modifications possibles jusqu’à ce que le bouton « Soumettre » soit cliqué.

---

## 🔧 Stack Technique

* **Backend** : ASP.NET Core MVC (.NET 8.0), Entity Framework Core
* **Frontend** : Razor Views + Tailwind CSS
* **Base de données** : Azure SQL Database
* **Stockage** : Azure Blob Storage
* **Outils de Développement** : Visual Studio Code / Visual Studio 2022, GitHub Actions
* **Hébergement & CI/CD** : Azure App Service, Azure DevOps / GitHub Actions

---

## 📂 Structure du Répertoire

```plaintext
ExAMina/
├── Controllers/                # Actions des contrôleurs ASP.NET MVC
├── Middleware/                 # Middleware personnalisé (suivi de l’activité)
├── Migrations/                 # Migrations Entity Framework Core
├── Models/                     # Classes de modèles Entity Framework Core
├── Services/                   # Logique métier et services auxiliaires
├── Views/                      # Vues Razor + Tailwind CSS
├── wwwroot/                    # Ressources statiques : CSS, JS, images
├── appsettings.json            # Configuration production (chaînes de connexion, etc.)
├── appsettings.Development.json# Paramètres pour le développement
├── Program.cs                  # Démarrage de l’application
├── AppDev2Project.csproj       # Fichier projet .NET
├── README.md                   # ← Vous êtes ici
└── Scrum.md                    # Notes sur le processus Agile/Scrum
```

---

## ⬇️ Installation & Démarrage

1. **Cloner le dépôt**

   ```bash
   git clone https://github.com/Alexandre-Scebba/AppDev2Project.git
   cd AppDev2Project
   ```

2. **Configurer l’environnement local**

   * Ouvrez `appsettings.Development.json` et mettez à jour :

     ```jsonc
     {
       "ConnectionStrings": {
         "DefaultConnection": "Server=<VOTRE_SERVEUR_SQL>;Database=<VOTRE_NOM_BD>;User Id=<UTILISATEUR>;Password=<MOT_DE_PASSE>;"
       },
       "AzureBlob": {
         "ConnectionString": "<VOTRE_CHAÎNE_AZURE_BLOB>",
         "ContainerName": "profile-pictures"
       }
       // ...autres paramètres de l’application
     }
     ```
   * Assurez-vous que votre base Azure SQL existe et que votre utilisateur a les droits nécessaires.
   * Créez le conteneur Azure Blob nommé `profile-pictures` ou ajustez `ContainerName`.

3. **Appliquer les migrations & remplir la base**

   ```bash
   dotnet ef database update
   ```

   * Optionnel : pour générer le modèle à partir d’une base existante

     ```bash
     dotnet ef dbcontext scaffold "Server=<...>;Database=<...>;" Microsoft.EntityFrameworkCore.SqlServer -o Models
     ```

4. **Construire & exécuter localement**

   ```bash
   dotnet build
   dotnet run
   ```

   * Par défaut, l’application s’exécute sur `https://localhost:5001` (SSL) et `http://localhost:5000`.
   * Ouvrez votre navigateur et accédez à l’URL racine.
   * Connectez-vous avec un compte administrateur ou créez un compte enseignant/étudiant si nécessaire.

---

## 🚧 Dépannage

* **Changements de schéma de base de données** :
  Après toute modification de modèle, exécutez

  ```bash
  dotnet ef migrations add <NomMigration>
  dotnet ef database update
  ```
* **Erreurs Azure Blob Storage** :
  Vérifiez la `ConnectionString` et le `ContainerName` dans `appsettings.json`.
  Ajoutez des logs (`ILogger`) dans `Services/ProfilePictureService` pour confirmer l’accès.
* **Fuseaux horaires / Timing** :
  ExAMina utilise UTC pour tous les horodatages.
  Si votre fuseau diffère, ajustez le format côté client ou serveur.
* **Fichiers statiques introuvables** :
  Assurez-vous que `app.UseStaticFiles()` est appelé dans `Program.cs`.
  Confirmez que Tailwind CSS est compilé :

  ```bash
  npm install
  npx tailwindcss -i ./wwwroot/css/site.css -o ./wwwroot/css/site.build.css
  ```

---

## 🔭 Travaux à Venir

* **Inscription & Authentification Avancées**

  * 2FA (e-mail/SMS)
  * Autorisation par rôle (Admin, Enseignant, Étudiant)
* **Rapports & Analyses**

  * Tableaux de bord et exports CSV/PDF
* **Notifications Améliorées**

  * Intégration Twilio/SendGrid, SignalR
* **Optimisation Mobile & PWA**

  * Améliorer la responsiveness, mode hors ligne
* **Gestion de Classe & Admin**

  * Création de classes, inscriptions groupées, paramètres globaux

---

## 📜 Licence

Ce projet est publié sous la **licence MIT**. Voir [LICENSE](LICENSE) pour plus de détails.

---

## ⭐ Comment Contribuer

1. **Fork** le dépôt sur GitHub
2. **Créer** une branche de fonctionnalité

   ```bash
   git checkout -b feature/<VotreFeature>
   ```
3. **Commit & Push**

   ```bash
   git commit -m "Ajout <feature>"
   git push origin feature/<VotreFeature>
   ```
4. **Ouvrir** une Pull Request contre `main`
5. Patientez la revue de code, intégrez les retours, puis fusionnez.

Merci pour vos contributions !


--------------------------------------------------
#ENG:

# ExAMina

> **ExAMina** is an Online Exam Management System built with ASP.NET Core MVC that empowers teachers to create, assign, and grade exams—and allows students to take and review them—on any device.

---

## 📝 Project Overview

ExAMina is a full-stack C# ASP.NET application designed for teachers and students to manage, distribute, and complete exams online. Core functionality includes:

* **Exam Creation & Editing** – Teachers define multiple-choice, true/false, and short-answer questions.
* **Assignment** – Instantly assign exams to groups of students.
* **Progress Tracking & Grading** – Teachers track completion status and grade exams; students receive automated notifications.
* **Responsive Front-End** – Built with Tailwind CSS and Razor/MVC views for a clean, mobile-friendly interface.
* **Cloud Integration** – Uses Azure SQL Database for exam data and Azure Blob Storage for profile picture uploads.
* **Notifications** – Built-in real-time updates and email notifications (planned).

---

## 🚀 Key Features

### For Teachers

1. **Create Various Question Types**

   * Supports Multiple-choice, True/False, and Short-Answer questions.
2. **Assign Exams to Student Groups**

   * Select classes or individual students for assignment.
3. **Track Student Progress**

   * Monitor who has started, is in progress, or has completed an exam.
4. **Grade & Provide Feedback**

   * Enter grades, leave comments, and release results to students.

### For Students

1. **View Pending & Completed Exams**

   * Dashboard lists exams that are available or already submitted.
2. **Take Exams on Any Device**

   * Responsive UI adapts to desktop and mobile devices.
3. **Edit Answers until Submission**

   * Changes allowed until the "Submit" button is clicked.

---

## 🔧 Tech Stack

* **Framework & Libraries**

  * ASP.NET Core MVC (.NET 8.0)
  * Entity Framework Core (ORM)
  * Tailwind CSS (UI styling)
* **Database & Storage**

  * Azure SQL Database (hosted in Azure)
  * Azure Blob Storage (for profile picture uploads)
* **Development Tools**

  * Visual Studio Code / Visual Studio 2022
  * GitHub (version control & CI/CD)
* **Hosting & Cloud Services**

  * Microsoft Azure App Service (web hosting)
  * Azure DevOps / GitHub Actions (build & deployment pipelines)

---

## 📂 Repository Structure

```
ExAMina/
├── Controllers/                # ASP.NET MVC controller actions
├── Middleware/                 # Custom middleware (e.g., LastActivity tracking)
├── Migrations/                 # EF Core migrations
├── Models/                     # Entity Framework Core model classes
├── Services/                   # Business logic and helper services
├── Views/                      # Razor views (HTML + Tailwind CSS)
├── wwwroot/                    # Static assets: CSS, JS, images
├── appsettings.json            # Production configuration (connection strings, etc.)
├── appsettings.Development.json# Local development settings
├── Program.cs                  # Application startup and DI configuration
├── AppDev2Project.csproj       # .NET project file
├── README.md                   # ← You are here
└── Scrum.md                    # Agile/Scrum process notes
```

---

## ⬇️ Installation & Setup

1. **Clone the repository**

   ```bash
   git clone https://github.com/Alexandre-Scebba/AppDev2Project.git
   cd AppDev2Project
   ```

2. **Configure your local environment**

   * Open `appsettings.Development.json` and update the following keys:

     ```jsonc
     {
       "ConnectionStrings": {
         "DefaultConnection": "Server=<YOUR_SQL_SERVER>;Database=<YOUR_DB_NAME>;User Id=<USERNAME>;Password=<PASSWORD>;"
       },
       "AzureBlob": {
         "ConnectionString": "<YOUR_AZURE_BLOB_CONNECTION_STRING>",
         "ContainerName": "profile-pictures"
       }
       // ...other app-specific settings
     }
     ```
   * Ensure your Azure SQL database exists and grant your user the correct permissions.
   * Create the Blob Storage container named `profile-pictures` in your Azure Storage account, or adjust `ContainerName` accordingly.

3. **Apply EF Core Migrations & Seed Database**
   From the project root:

   ```bash
   dotnet ef database update
   ```

   * To scaffold from an existing database (optional):

     ```bash
     dotnet ef dbcontext scaffold "Server=<...>;Database=<...>;" Microsoft.EntityFrameworkCore.SqlServer -o Models
     ```

4. **Build & Run Locally**

   ```bash
   dotnet build
   dotnet run
   ```

   * By default, the app runs at `https://localhost:5001` (SSL) and `http://localhost:5000` (HTTP).
   * Open your browser and navigate to the root URL.
   * Log in with a seeded admin account or register a new teacher/student account if registration is enabled.

---

## 🚧 Troubleshooting

### Database Schema Changes

* If the `Users` table is renamed or altered (e.g., from `AspNetUsers`), update the `ApplicationUser` model’s `UserName` mapping accordingly.
* Always run `dotnet ef migrations add <MigrationName>` after modifying any model class.
* Use `dotnet ef database update` to sync the database with the latest model.

### Azure Blob Storage Errors

* Verify the **ConnectionString** and **ContainerName** in `appsettings.json`.
* Add logging (e.g., `ILogger`) in `Services/ProfilePictureService` to confirm the container can be accessed.
* Check CORS settings on your Storage account if images do not load in the browser.

### Time Zone / Exam Timing Issues

* ExAMina uses UTC for all server-side date/times.
* If your local time zone differs, adjust client-side JavaScript or server formatting so students see correct exam start/end times.

### Static Files Not Loading

* Ensure `app.UseStaticFiles()` is called in `Program.cs`.
* Confirm that Tailwind CSS has been built—run `npm install` then:

  ```bash
  npx tailwindcss -i ./wwwroot/css/site.css -o ./wwwroot/css/site.build.css
  ```

  if you modify `tailwind.config.js`.

---

## 🔭 Future Work

* **Advanced Registration & Authentication**

  * Implement two-factor authentication (2FA) via email/SMS.
  * Role-based authorization for “Admin,” “Teacher,” and “Student” levels.

* **Deep Reporting & Analytics**

  * Add dashboards showing exam performance metrics over time.
  * Exportable CSV/PDF reports for administrators.

* **Enhanced Notifications**

  * Integrate Twilio/SendGrid for SMS and email alerts when grades are posted.
  * In-app push notifications via SignalR.

* **Mobile Optimization**

  * Refine responsive breakpoints to ensure flawless experience on phones/tablets.
  * Consider a lightweight PWA wrapper for offline exam review.

* **Class & Admin Controls**

  * Enable “Class” creation, student roster management, and bulk exam assignment.
  * Admin panel for site-wide settings (themes, default timeouts, etc.).

---

## 📜 License

This project is released under the **MIT License**. 

---

## ⭐ How to Contribute

1. **Fork** the repository on GitHub.
2. **Create** a feature branch:

   ```bash
   git checkout -b feature/<YourFeature>
   ```
3. **Commit** your changes and push to your fork:

   ```bash
   git commit -m "Add <feature> / fix <bug>"
   git push origin feature/<YourFeature>
   ```
4. **Open** a Pull Request against `main`.
5. Wait for code review, address feedback, and merge once approved.

Thank you for helping improve ExAMina!
