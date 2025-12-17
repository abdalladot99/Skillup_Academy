# Bedaya Learning Platform (ASP.NET MVC · .NET 8)

> A clean, well-structured learning platform built with **ASP.NET MVC (.NET 8)** using an **N-Tier architecture** (Presentation ▶︎ BLL ▶︎ DAL ▶︎ Database). The platform includes three roles — **Admin**, **Instructor**, and **Student** — each with dedicated dashboards and role-specific permissions.

---

## 🚀 Quick Highlights

* ✅ **N‑Tier Architecture** — Presentation / BLL / DAL / Database
* 👤 **Roles** — Admin, Instructor, Student (separate dashboards & permissions)
* 💳 **Payments** — PayMob integrated; easy to add PayPal, Fawry, wallets
* 🔎 **Search & Filters** — Advanced search for courses, instructors, categories
* 📦 **Subscription System** — Single subscription type with admin-controlled limits
* 🎬 **Media** — Upload video lessons (on-disk or cloud storage)
* 🔒 **Security** — Role-based authorization and best practices

---

## 🔑 Seed Admin (Development)

> Use this seeded admin account for local development / testing. **Do not** use these credentials in production — change them or store secrets securely.

* **Email:** `admin@gmail.com`
* **Password:** `Admin@123`

---

## 🏗️ Architecture (N‑Tier) — Overview

```
Presentation (ASP.NET MVC)
    ⇅
Business Logic Layer (Services, Validation, DTOs)
    ⇅
Data Access Layer (Repositories, EF Core DbContext)
    ⇅
Database (SQL Server)
```

### Layers — Responsibilities

---
* **Presentation Layer**

  * MVC Controllers, Views, ViewModels
  * Thin controllers — delegate logic to BLL

* **Business Logic Layer (BLL)**

  * Core application rules, services, business validation
  * Interfaces for payment, storage, and search
  * DTOs and mapping (AutoMapper)

* **Data Access Layer (DAL)**

  * EF Core repositories, unit-of-work, migrations
  * Implementation of storage, seeding, and query optimizations

* **Database**

  * SQL Server with migrations & seed data

---

## ⚙️ Getting Started (Developer)

### Prerequisites

* .NET 8 SDK
* SQL Server / LocalDB
* Visual Studio 2022+ or VS Code

### Quick Setup

1. Clone repo

```bash
git clone https://github.com/abdalladot99/Skillup_Academy.git
cd bedaya-learning-platform
```

2. Configure connection string & keys in `appsettings.Development.json` or user secrets
3. Apply EF migrations & seed data

```bash
dotnet ef database update --project src/Your.DAL/Your.DAL.csproj --startup-project src/Your.Presentation/Your.Presentation.csproj
```

4. Run the web project

```bash
dotnet run --project src/Your.Presentation/Your.Presentation.csproj
 
```

---

## 🔐 Configuration (Important)

appsettings.json and appsettings.Development.json are not included in the repository for security reasons.

You must create them manually before running the project.

📄 Create appsettings.Development.json

Inside the Presentation (MVC) project, create:

appsettings.Development.json


Then add:

{
  "PaymobSettings": {
    "ApiKey": "YOUR_PAYMOB_API_KEY",
    "IframeId": "YOUR_IFRAME_ID",
    "IntegrationId": "YOUR_INTEGRATION_ID",
    "BaseUrl": "https://accept.paymob.com/api",
    "Hmac": "YOUR_PAYMOB_HMAC"
  },

  "SMTP": {
    "Host": "smtp.gmail.com",
    "Port": "587",
    "User": "YOUR_EMAIL@gmail.com",
    "Pass": "YOUR_APP_PASSWORD",
    "From": "Bedaya_Platform@gmail.com"
  },

  "ConnectionStrings": {
    "cs": "Server=.;Database=BedayaDb;Trusted_Connection=True;TrustServerCertificate=True"
  },

  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },

  "AllowedHosts": "*"
}

🧾 Configuration Sections
PaymobSettings

Payment gateway configuration

SMTP

Used for email confirmation & notifications

Gmail requires App Password

ConnectionStrings

SQL Server database connection
---

## 🔌 Extensibility Points

* **Payments:** Implement `IPaymentGateway` to add PayPal, Fawry, or wallets.
* **Storage:** Swap local file storage with Azure Blob / AWS S3 by replacing the storage provider.
* **Search:** Replace or augment DB search with Elasticsearch for large scale.
* **Multitenancy:** Add tenant-aware data filtering in DAL and BLL.

---

## 🧩 Roles & Permissions — Summary

* **Admin** — Full CRUD on users, courses, categories, subscriptions, payments
* **Instructor** — Manage own courses, lessons, uploads, view analytics for their courses
* **Student** — Browse / enroll / consume content according to subscription limits

---

## 🛠 Development Tips

* Keep controllers thin; place business rules in BLL
* Use DTOs and AutoMapper for mapping domain models
* Store credentials securely (User Secrets / Key Vault) for production
* Seed admin and sample data only in development environments

---

## 📬 Contact / Author

**Author:** Abdalla mohammed

**Readme:** https://github.com/abdalladot99
