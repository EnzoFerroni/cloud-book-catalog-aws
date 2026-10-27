# Biblioteca AWS

[![Java](https://img.shields.io/badge/Java-Spring%20Boot-6DB33F?logo=springboot&logoColor=white)](https://spring.io/projects/spring-boot)
[![React](https://img.shields.io/badge/React-18-61DAFB?logo=react&logoColor=black)](https://react.dev)
[![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?logo=docker&logoColor=white)](https://docs.docker.com/compose/)
[![AWS](https://img.shields.io/badge/AWS-EC2-FF9900?logo=amazonwebservices&logoColor=white)](https://aws.amazon.com/ec2/)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)

A containerized book catalog with a Spring Boot API and a React front end, built to be deployed on AWS.

## Table of Contents

- [About](#about)
- [Architecture](#architecture)
- [Getting Started](#getting-started)
- [Deploying on AWS](#deploying-on-aws)
- [Project Structure](#project-structure)
- [Team](#team)
- [License](#license)

## About

Final version of the first project of a cloud services course at Universidade
Presbiteriana Mackenzie (2024). The goal was to split an application into a back-end
and a front-end container and run each one on its own cloud machine. An earlier
iteration lives in [cloud-book-catalog-v1](https://github.com/EnzoFerroni/cloud-book-catalog-v1).

## Architecture

| Service | Stack | Port |
| --- | --- | --- |
| `backend` | Spring Boot REST API, `GET /books` returns the catalog | 25000 |
| `frontend` | React (Create React App) page that lists the books as cards | 8080 |

Each service has its own `Dockerfile` and `compose.yaml`, so they can run on separate
hosts.

## Getting Started

Requirements: Docker with Compose.

```bash
git clone https://github.com/EnzoFerroni/cloud-book-catalog-aws.git
cd cloud-book-catalog-aws

(cd backend && docker compose up --build -d)
(cd frontend && docker compose up --build -d)
```

Open http://localhost:8080. The API answers on http://localhost:25000/books.

## Deploying on AWS

1. Launch two EC2 instances with Docker installed and open ports 25000 and 8080 in
   their security groups.
2. Run the back-end container on the first instance and the front-end container on
   the second.
3. In `frontend/src/App.js`, replace `localhost` in the `fetch` URL with the back-end
   instance's public IP before building the front-end image.

## Project Structure

```
├── backend/    Spring Boot API, Dockerfile, compose.yaml
└── frontend/   React app, Dockerfile, compose.yaml
```

## Team

- Enzo Ferroni ([@EnzoFerroni](https://github.com/EnzoFerroni))
- Rafael Neves
- Rodrygo Vasconcellos

## License

Released under the [MIT License](LICENSE). Copyright (c) 2024 Enzo Ferroni, Rafael
Neves and Rodrygo Vasconcellos.
