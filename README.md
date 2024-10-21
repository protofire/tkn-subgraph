# TKN Subgraph

## Table of Contents

- [Installation Prerequisites](#installation-prerequisites)
- [Running the Subgraph Locally with Docker Compose](#running-the-subgraph-locally-with-docker-compose)
- [How to Deploy a Subgraph Using TKN Hosted Service](#how-to-deploy-a-subgraph-using-tkn-hosted-service)
- [Additional Resources](#additional-resources)

## Installation Prerequisites

### How to Install Node.js and npm

- **Description:** Node.js is a server platform for running JavaScript, which includes npm (Node Package Manager).
- **Usage:** Required for installing dependencies and running development tools like Graph CLI.
- **Installation:** Download and install Node.js and npm from the official website:
  - [Download Node.js](https://nodejs.org/en/)

### How to Install Yarn

- **Description:** Yarn is an alternative to npm for managing project dependencies. It is used for fast and reliable package installation.
- **Installation:** Install Yarn via npm:
  ```bash
  npm install -g yarn
  ```

### How to Install Docker and Docker Compose

- **Description:** Docker is a containerization platform that allows running applications in isolated containers. Docker Compose is a tool for managing multi-container applications.
- **Usage:** Used for deploying services like IPFS, Postgres, and Graph Node, which are necessary for running subgraphs locally.
- **Installation:** Download and install Docker from the official website:
  - [Download Docker](https://www.docker.com/products/docker-desktop)
 
### How to Install Graph CLI

- **Description:** Graph CLI is a command-line tool for creating, building, and deploying subgraphs.
- **Installation:** Install Graph CLI via npm:
  ```bash
  npm install -g @graphprotocol/graph-cli
  ```
  
## Running the Subgraph Locally with Docker Compose

### Prerequisites

Before running the subgraph locally, ensure that you have installed the following:

- [Node.js and npm](#how-to-install-nodejs-and-npm)
- [Yarn](#how-to-install-yarn)
- [Docker and Docker Compose](#how-to-install-docker-and-docker-compose)
- [Graph CLI](#how-to-install-graph-cli)

### Step 1: Clone the Repository

```bash
git clone https://github.com/protofire/tkn-subgraph
cd tkn-subgraph
```
### Step 2: Start the Docker Services

Start the necessary services (IPFS, Postgres, and Graph Node) using Docker Compose:

```bash
docker-compose up -d
```

This command will start the following services:

- **IPFS**: InterPlanetary File System for decentralized file storage.
- **Postgres**: Database service for storing indexed data.
- **Graph Node**: The service responsible for indexing and serving queries.

### Step 3: Build the Subgraph

You should clone your subgraph repo:

git clone https://github.com/your-subgraph/repo
ce repo

```bash
yarn install
graph codegen
graph build
```

### Step 4: Deploy Your Subgraph Locally

Once the services are running, you can deploy your subgraph locally:

```bash
graph create --node http://localhost:8020/ <your-subgraph-name>
graph deploy <your-subgraph-name> --ipfs http://localhost:5001 --node http://localhost:8020/
```

Replace `<your-subgraph-name>` with the name of your subgraph.

Alternatively, you can use the following yarn scripts:

```bash
yarn create-local
yarn deploy-local
```

### Step 5: Querying the Subgraph

After deployment, you can query your subgraph using the following GraphQL endpoint:

```
http://localhost:8000/subgraphs/name/<your-subgraph-name>
```

## How to Deploy a Subgraph Using TKN Hosted Service

TKN Hosted Services (TKN-HS) for The Graph is a platform that let you deploy subgraphs in our infrastructure.

|          | Endpoints                  | Explanation                                                  |
|----------|----------------------------|--------------------------------------------------------------|
| Index    | https://index.graph.tkn.xyz | This endpoint is used to deploy the subgraph.                |
| Query    | https://query.graph.tkn.xyz | This endpoint is used to get data from the subgraph.         |
| IPFS     | https://ipfs.graph.tkn.xyz  | This endpoint is used to store data builded by the subgraph. |
| Grafana  | https://grafana.graph.tkn.xyz  | Monitoring dashboards for The Graph                          |  


### Prerequisites

Before deploying the subgraph using the TKN Hosted Service, ensure that you have installed the following:

- [Node.js and npm](#how-to-install-nodejs-and-npm)
- [Yarn](#how-to-install-yarn)
- [Graph CLI](#how-to-install-graph-cli)

### Step 1: Download the Repository

```bash
git clone https://github.com/your-subgraph/repo
cd repo
```

### Step 2: Build the Subgraph

```bash
yarn install
graph codegen
graph build
```

### Step 3: Deploy the Subgraph

Once you have your credentials (user and password), you can deploy the subgraph:

```bash
graph create --node https://user:password@index.graph.tkn.xyz tkn/example1
graph deploy tkn/example1 --version-label tkn/example1 --headers "{\"Authorization\": \"Basic user:password encoded\"}" --ipfs https://ipfs.graph.tkn.xyz --node https://user:password@index.graph.tkn.xyz
```

## Additional Resources

For more information about subgraphs, visit The Graph documentation:

[The Graph Documentation](https://thegraph.com/docs/en/developing/creating-a-subgraph/)

