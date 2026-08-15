```markdown
# Bulky — E-Commerce Book Store

A full-featured ASP.NET Core MVC e-commerce application for browsing and purchasing books, built with a multi-tier architecture and role-based access control.

## Overview

Bulky is a web application that simulates a real-world online bookstore. It supports two main user experiences: a customer-facing storefront for browsing products and checking out, and an admin panel for managing inventory, orders, users, and companies. The project was built to practice production-style architecture patterns rather than a simple CRUD demo.

## Features

- **Role-based access control** with four roles (Admin, Employee, Company, Customer), each with a different level of access to the system
- **Product management** with full CRUD operations, including multi-image upload per product
- **Shopping cart** with session-based cart tracking and live cart count
- **Order management** with order status tracking (Pending, Approved, Processing, Shipped, Cancelled, Refunded)
- **Stripe integration** for secure checkout and payment processing
- **Authentication** via ASP.NET Core Identity, with Facebook login support
- **Company accounts** with delayed payment workflow, separate from individual customer checkout
- **Admin dashboard** for managing categories, companies, products, orders, and users

## Architecture

The solution follows an N-Tier architecture, splitting responsibilities across separate class libraries instead of putting everything in the web project:

- **Bulky.Models** — Entity classes and view models
- **Bulky.DataAccess** — DbContext, EF Core migrations, Repository pattern, and Unit of Work implementation
- **Bulky.Utility** — Shared constants and settings (roles, status strings, Stripe settings)
- **BulkyWeb** — MVC application (Controllers, Views, Areas, ViewComponents)

This separation keeps the data access logic decoupled from the presentation layer and makes the codebase easier to test and extend.

## Tech Stack

- ASP.NET Core MVC (.NET 8)
- Entity Framework Core
- SQL Server
- ASP.NET Core Identity
- Stripe API
- Bootstrap

## Getting Started

### Prerequisites

- .NET 8 SDK
- SQL Server (LocalDB or full instance)
- Visual Studio 2022 (recommended) or any editor with .NET support

### Setup

1. Clone the repository
   ```
   git clone https://github.com/amrrummaneh/Bulky.git
   ```

2. Update the connection string in `BulkyWeb/appsettings.json` to point to your local SQL Server instance.

3. Set up your own Stripe and Facebook credentials using .NET User Secrets (keeps them out of source control):
   ```
   cd BulkyWeb
   dotnet user-secrets init
   dotnet user-secrets set "Stripe:SecretKey" "your-secret-key"
   dotnet user-secrets set "Stripe:PublishableKey" "your-publishable-key"
   dotnet user-secrets set "Authentication:Facebook:AppId" "your-app-id"
   dotnet user-secrets set "Authentication:Facebook:AppSecret" "your-app-secret"
   ```

4. Apply the migrations:
   ```
   dotnet ef database update --project Bulky.DataAccess --startup-project BulkyWeb
   ```

5. Run the application:
   ```
   dotnet run --project BulkyWeb
   ```

The database is seeded automatically on first run with an admin account (see `DbInitializer`).

## Notes

This project was built as a learning exercise to apply N-Tier architecture, the Repository/Unit of Work pattern, and payment integration in a realistic setting, rather than as a production deployment.
```
