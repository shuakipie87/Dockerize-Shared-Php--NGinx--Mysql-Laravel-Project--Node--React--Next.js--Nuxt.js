# Multi-Laravel Docker Setup with Inertia

This repository provides a **professional Docker-based development environment** for running multiple Laravel 12 projects simultaneously, including Laravel with Inertia.js. It uses **shared PHP, Node, Composer, MySQL containers** and a **Traefik reverse proxy** to manage multiple apps without port conflicts.

---

## 🚀 Features

- Multiple Laravel apps running at the same time
- Shared PHP/Node/Composer Docker image
- Shared MySQL container
- Traefik reverse proxy for automatic subdomain routing
- Fully containerized — no local PHP, Composer, or Node installation required
- Each app has its own `.env` and Nginx configuration
- Dynamic new project creation with one command
- Scalable architecture suitable for teams or production-like development

---

## 🗂 Folder Structure

```text
docker-laravel/
│
├── shared/
│   ├── php/
│   │   └── Dockerfile
│   └── mysql/
│       └── docker-compose.yml
│
├── apps/
│   ├── template/               # Template for new projects
│   ├── laravel-project-1/
│   └── laravel-project-2/
│
├── new-laravel-project.sh      # Script to create new Laravel apps
└── docker-compose.yml          # Root compose with Traefik + shared network
⚙️ Prerequisites
Docker Desktop

Git

Basic knowledge of Docker and Laravel

🛠 Setup Instructions
1. Clone the repository
bash
Copy code
git clone <your-repo-url>
cd docker-laravel
2. Create the shared Docker network
bash
Copy code
docker network create laravel || true
3. Start Traefik and shared services
bash
Copy code
docker compose up -d
🔧 Dynamic New Project Creation
Use the included Bash script new-laravel-project.sh to create new Laravel apps dynamically.

1. Make the script executable
bash
Copy code
chmod +x new-laravel-project.sh
2. Create a new Laravel project
Plain Laravel 12:

bash
Copy code
./new-laravel-project.sh laravel-new
Laravel + Inertia (Vue 3):

bash
Copy code
./new-laravel-project.sh laravel-inertia inertia
The script will automatically:

Copy the apps/template folder to a new project folder

Update .env with the project name and database

Create a database in MySQL

Spin up Docker containers

Install Laravel (and Inertia if requested)

3. Access your new project
Traefik automatically routes based on the project name:

arduino
Copy code
http://laravel-new.localhost
http://laravel-inertia.localhost
Make sure to add these to /etc/hosts or your OS equivalent:

cpp
Copy code
127.0.0.1 laravel-new.localhost
127.0.0.1 laravel-inertia.localhost
🔗 Configure Template Project
The apps/template folder contains:

.env (with placeholder values)

docker-compose.override.yml

nginx/default.conf

This folder is copied for every new project, so you don’t have to edit any Docker or Nginx settings manually.

💡 Laravel Environment Example
Example .env for a new Laravel project:

env
Copy code
PROJECT_NAME=laravel-new
DB_CONNECTION=mysql
DB_HOST=mysql_db
DB_PORT=3306
DB_DATABASE=laravel_new
DB_USERNAME=laravel
DB_PASSWORD=secret
🧰 Useful Docker Commands
bash
Copy code
# List running containers
docker ps

# Run artisan commands inside a project container
docker exec -it laravel-new_app php artisan migrate

# Stop a project
docker compose down
✅ Benefits
Truly dynamic — copy the template folder to create new projects

No port or container conflicts — Traefik handles routing

Fully containerized — PHP, Node, Composer, MySQL are reused

Inertia-ready — just pass the inertia flag when creating a project

Production-like development environment

