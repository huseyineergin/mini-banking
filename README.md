# Mini Banking Application

Description.

## Table of Contents

- [Overview](#overview)
- [Technology](#technology)
- [Getting Started](#getting-started)
- [API Endpoints](#api-endpoints)
- [Postman](#postman)

## Overview

The application is composed of three main services:

- Client: A NextJS application that serves as the user interface.
- Server: A Spring Boot application that provides the backend logic and API.
- Database: A MySQL database to store application data.

The client and server applications are included as Git submodules:

- Client: `https://github.com/huseyineergin/mini-banking-client.git`
- Server: `https://github.com/huseyineergin/mini-banking-server.git`

## Technology

### Backend (mini-banking-server)

- Java 21
- Spring Boot 3
- MySQL 8.4
- Swagger

### Frontend (mini-banking-client)

- React 19
- NextJS 15
- TypeScript
- Tailwind CSS

## Getting Started

The application runs in Docker containers, orchestrated by `docker-compose`. The services are defined in the `docker-compose.yaml` file.

### Prerequisites

Ensure you have the following installed:

- Docker
- Docker Compose

### Services

#### Client (next)

- Container Name: `mini-banking-client`
- Image: `mini-banking-client`
- Ports: `3000:3000`
- Environments:
  - `JWT_SECRET`: `Zh28h8kvun73MrRyY82fwR3FXMvBUTpd`
  - `API_BASE_URL`: `http://java:5000`

#### Server (java)

- Container Name `mini-banking-client`
- Image: `mini-banking-client`
- Ports: `5000:5000`
- Environments:
  - `DB_HOST`: `mysql`
  - `DB_DRIVER`: `com.mysql.cj.jdbc.Driver`
  - `DB_USERNAME`: `mini-banking-user`
  - `DB_PASSWORD`: `P2LHrNj4RcNwqY`
  - `JWT_SECRET`: `Zh28h8kvun73MrRyY82fwR3FXMvBUTpd`
  - `JWT_EXPIRATION`: `3600000`

#### Database (mysql)

- Container Name: `mini-banking-mysql`
- Image: `mysql:8.4`
- Ports: `3306:3306`
- Environments:
  - MYSQL_USER: `mini-banking-user`
  - MYSQL_PASSWORD: `P2LHrNj4RcNwqY`
  - MYSQL_DATABASE: `mini-banking-db`
  - MYSQL_ROOT_PASSWORD: `D547ish6Kq74ft`

### How to Run?

1. Clone the repository and submodules:

```bash
git clone --recurse-submodules https://github.com/huseyineergin/mini-banking.git
```

2. Navigate to the root directory of the project:

```bash
cd mini-banking
```

3. Run the application using Docker Compose:

```bash
docker-compose up -d --build
```

On startup, the application creates 2 users with 3 accounts each:

- John Doe:

  - Username: john.doe
  - Password: 12345aA+
  - Email: `john.doe@example.com`

- Jane Doe:
  - Username: jane.doe
  - Password: 12345aA+
  - Email: `jane.doe@example.com`

## API Endpoints

The API endpoints are defined in the Postman collections and can also be explored on [Swagger UI](http://localhost:5000/swagger-ui/index.html).

### User API

- **POST** `/api/users/register`: Register a new user.
- **POST** `/api/users/login`: Authenticate a user.

### Account API

- **POST** `/api/accounts`: Create a new account.
- **POST** `/api/accounts/search`: Get a list of accounts.
- **PUT** `/api/accounts/{id}`: Update an account.
- **DELETE** `/api/accounts/{id}`: Delete an account.
- **GET** `/api/accounts/{id}`: Get account details.

### Transaction API

- **POST** `/api/transactions/transfer`: Initiate a money transfer.
- **GET** `/api/transactions/account/{id}`: View transaction history for an account.

## Postman

Postman collections are provided to test the API endpoints. They can be found in the `postman-collection` directory.

- user.postman_collection.json
- account.postman_collection.json
- transfer.postman_collection.json
