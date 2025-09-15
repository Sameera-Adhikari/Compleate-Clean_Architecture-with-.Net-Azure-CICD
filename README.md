# FinanceApp (Angular + .NET + Azure)

This repository contains the FinanceApp project:
- **Frontend:** Angular 13
- **Backend:** .NET (Clean Architecture with Api, Domain, Application, Infrastructure, Migrations). Mediator and Repository Patters. Identity server for authentication and authorization, EF core for data manipulation
- **Database:** Azure SQL
- **API Gateway:** Azure API Management (APIM)
- **CI/CD:** Bitbucket Pipelines 
                Runs build + test on all branches.
                Deploys Simulation when pushing to release/sim.
                Deploys Production (manual approval) when pushing to release/production.

---

## Project Structure

src/
ApiGateway/
FinanceApp.Api/
FinanceApp.Application/
FinanceApp.Domain/
FinanceApp.Infrastructure/
FinanceApp.Migrations/
test/
FinanceApp.Tests/
finance-app-ui/


---

## Branching Strategy
- `master` → development baseline (build/test only).
- `release/sim` → deploys to Simulation environment.
- `release/production` → deploys to Production (manual approval required).

---

## Local Development

### Develop new feature

git checkout master
git pull
git checkout -b feature/add-login
--develop, commit, push--
git push origin feature/add-login

Open PR → merge into master.

CI runs build + tests, but no deploy.

### Promote to Simulation

git checkout release/sim
git pull
git merge master
git push origin release/sim

CI builds backend + frontend, runs unit tests, deploys to Azure Simulation.

### Promote to Production

git checkout release/production
git pull
git merge release/sim
git push origin release/production

### Backend
```bash
cd src
dotnet restore
dotnet build
dotnet run --project FinanceApp.Api
dotnet run --project FinanceApp.ApiGateway
dotnet test ./../test/FinanceApp.Tests
```
### Frontend
```bash
cd finance-app-ui
npm install
ng serve --open
```

---

## Commit files to Git

git add .gitignore bitbucket-pipelines.yml README.md
git commit -m "Add gitignore, CI/CD pipeline, and README"
git push origin master

Once pushed, Bitbucket will automatically detect bitbucket-pipelines.yml and enable pipelines.

---
