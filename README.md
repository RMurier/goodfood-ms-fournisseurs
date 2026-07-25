# goodfood-ms-fournisseurs

Supplier management microservice for the [GoodFood](https://github.com/RMurier/BAC-5-CUBE-1-COLLABORATIF) platform.

**Status:** 🚧 Scaffold — this is currently an unmodified `dotnet new webapi` template (only the sample `/weatherforecast` endpoint). No supplier-management logic has been written yet. See [`goodfood-ms-auth`](https://github.com/RMurier/goodfood-ms-auth#readme) for what a fleshed-out service in this platform looks like.

## Table of Contents

- [Intended Purpose](#intended-purpose)
- [Tech Stack](#tech-stack)
- [Environment Variables](#environment-variables)
- [Running Locally](#running-locally)
- [Tests](#tests)
- [CI/CD](#cicd)

## Intended Purpose

Own supplier accounts and deliveries that feed into `ms-stock`'s inventory levels.

## Tech Stack

- .NET 9 / ASP.NET Core Web API
- SQL Server, via `Microsoft.EntityFrameworkCore.SqlServer` (not yet added — connection string is wired up, no `DbContext` exists yet)

## Environment Variables

| Variable | Description |
|----------|--------------|
| `ASPNETCORE_ENVIRONMENT` | `Development` or `Production` |
| `ConnectionStrings__DefaultConnection` | SQL Server connection string (database `GoodFood_Fournisseurs_Dev` in dev) |

## Running Locally

### Via the platform's docker-compose

From the [parent repo](https://github.com/RMurier/BAC-5-CUBE-1-COLLABORATIF):

```bash
docker compose -f docker-compose.dev.yml up -d db-sql-dev ms-fournisseurs-dev
```

Runs on `http://localhost:3010`, Swagger at `http://localhost:3010/swagger`.

### Standalone

```bash
cd GoodFood.Fournisseurs.Api
dotnet restore
dotnet run
```

## Tests

```bash
dotnet test GoodFood.Fournisseurs.Tests/GoodFood.Fournisseurs.Tests.csproj --verbosity normal
```

Currently a single sanity check ([`SanityTests.cs`](GoodFood.Fournisseurs.Tests/SanityTests.cs)), there to keep the CI test job green while the service is empty.

## CI/CD

Built, scanned (SonarQube, Trivy, OWASP Dependency-Check, GitGuardian) and published on every push, gated on all of them passing — see the [parent repo's CI/CD Pipeline section](https://github.com/RMurier/BAC-5-CUBE-1-COLLABORATIF#cicd-pipeline) for how the pipeline is wired across repos.

Note: the SonarQube project key for this service is `goodfood-ms-fournisseur` (singular) rather than the plural used everywhere else — a historical naming inconsistency from when the SonarQube project was first created, kept as-is to avoid losing analysis history.
