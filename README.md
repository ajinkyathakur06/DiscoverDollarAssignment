# Discover Dollar Assignment -- MEAN Stack CRUD Application

This project demonstrates a full-stack CRUD application built using the
MEAN stack (MongoDB, Express, Angular 15, Node.js) and deployed using
modern DevOps practices including Docker, Nginx reverse proxy, AWS EC2,
and GitHub Actions CI/CD.

------------------------------------------------------------------------

# Application Overview

The application manages a collection of tutorials.

Each tutorial contains:

-   ID\
-   Title\
-   Description\
-   Published Status

Users can:

-   Create tutorials\
-   Retrieve all tutorials\
-   Retrieve a single tutorial\
-   Update tutorials\
-   Delete tutorials\
-   Search tutorials by title

------------------------------------------------------------------------

# Local Development Setup

## Backend (Node.js + Express)

``` bash
cd backend
npm install
node server.js
```

Configure MongoDB in:

backend/app/config/db.config.js

Backend runs on:

http://localhost:8080

------------------------------------------------------------------------

## Frontend (Angular 15)

``` bash
cd frontend
npm install
ng serve --port 8081
```

Modify API interaction inside:

frontend/src/app/services/tutorial.service.ts

Frontend runs on:

http://localhost:8081

------------------------------------------------------------------------

# Dockerized Deployment

The entire application is containerized using Docker and orchestrated
with Docker Compose.

## Services

-   MongoDB (mongo:6 official image)
-   Backend (Node.js + Express)
-   Frontend (Angular production build)
-   Nginx (Reverse proxy)
-   Docker Compose

## Run Using Docker

From project root:

``` bash
docker compose up -d
```

Application will be accessible at:

http://localhost

------------------------------------------------------------------------

# Nginx Reverse Proxy

Nginx is configured to expose the entire application via port 80.

Only Nginx is publicly exposed. Backend (8080) and MongoDB (27017)
remain internal to Docker network.

## Nginx Configuration

default.conf:

``` nginx
server {
    listen 80;

    location / {
        proxy_pass http://frontend:80;
    }

    location /api/ {
        proxy_pass http://backend:8080/api/;
    }
}
```

Routing:

-   `/` → Angular frontend\
-   `/api` → Backend REST API\
-   MongoDB → Internal only

------------------------------------------------------------------------

# AWS EC2 Deployment

The application is deployed on an Ubuntu EC2 instance.

## Deployment Steps

1.  Clone repository on EC2:

``` bash
git clone https://github.com/ajinkyathakur06/DiscoverDollarAssignment
cd DiscoverDollarAssignment
```

2.  Install Docker & Docker Compose

3.  Run:

``` bash
docker compose up -d
```

Application is accessible via:

http://`<EC2_PUBLIC_IP>`{=html}

------------------------------------------------------------------------

# Docker Hub

Images are pushed to Docker Hub:

ajinkya06/discoverdollarassignment

Tags include:

-   backend-latest\
-   frontend-latest\
-   Versioned tags (v1, v2, v3, etc.)

------------------------------------------------------------------------

# CI/CD Pipeline (GitHub Actions)

On every push to the main branch:

1.  Backend and frontend Docker images are built
2.  Images are tagged with version number and latest
3.  Images are pushed to Docker Hub
4.  GitHub Actions connects to EC2 via SSH
5.  Runs: docker compose pull docker compose up -d

This enables automated continuous deployment.

------------------------------------------------------------------------

# Architecture Overview

Client (Browser)\
↓\
Port 80\
↓\
Nginx\
↓\
Frontend & Backend\
↓\
MongoDB

------------------------------------------------------------------------

# Tech Stack

-   Angular 15\
-   Node.js\
-   Express.js\
-   MongoDB\
-   Docker\
-   Docker Compose\
-   Nginx\
-   GitHub Actions\
-   AWS EC2

------------------------------------------------------------------------

# Author

Ajinkya Thakur