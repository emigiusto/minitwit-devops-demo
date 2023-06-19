# Node.js Tweeting App with Monitoring and Logging on Docker Swarm

This repository contains a Dockerized Node.js tweeting application along with Dockerfiles and configuration files for monitoring and logging using Filebeat, Grafana, Prometheus, Elastic Search, and Kibana. Additionally, it includes Terraform configuration to deploy the project in a DigitalOcean Spaces bucket.

## Table of Contents
- [Description](#description)
- [Installation](#installation)
- [Usage](#usage)
- [Monitoring and Logging](#monitoring-and-logging)
- [Deployment](#deployment)

## Description

The repository provides a simple Node.js tweeting application that allows users to post tweets. It leverages Docker to containerize the application, making it easy to deploy and manage across different environments.

**Docker swarm** is used to run and maintain the containers.

The repository also includes Dockerfiles and configuration files for the following components:

1. **Filebeat**: A lightweight log shipper that collects and forwards logs.
2. **Grafana**: A powerful open-source monitoring and visualization platform.
3. **Prometheus**: A leading open-source monitoring and alerting toolkit.
4. **Elastic Search and Kibana**: A popular combination for searching, analyzing, and visualizing data in real-time.

Furthermore, it includes Terraform configuration files to deploy the project in a DigitalOcean Spaces bucket. This enables seamless infrastructure provisioning and management.

## Installation

To get started, clone the repository to your local machine:

```bash
git clone https://github.com/emigiusto/minitwit-devops-demo.git
cd minitwit-devops-demo
```

## Local Usage

### Running the Node.js Tweeting App

Before running the Node.js tweeting app, make sure you have [Docker](https://www.docker.com/get-started) installed on your system.

To build and run the Docker container for the tweeting app, use the following command:

```bash
docker-compose up -d
```

This command will build the Docker image and start the container in detached mode.

### Logging Setup

#### Filebeat
Filebeat is used to collect and forward logs from the Node.js minitwit app to Elastic search.

Filebeat will be built automatically 


### Monitoring Setup

#### Grafana + Prometheus

From `/minitwit-devops-demo/` run: 
```
docker-compose -f ./docker-compose-monitoring.yml up -d --build
```
And follow this steps:
1. Access 
        `http://localhost::3005/`
2. Enter basic credentials (admin, admin)
3. Go to Datasources > Add new Datasource
    Choose any name
    Type: Prometheus
    Url: `http://localhost:9090`
    Access: direct
    Click Add
4. Go to Dashboards
   Look for "Import Dashboard" in the top menu
   Copy the content of the file in `/grafana/dashboard.json`


## Deployment
The repository includes Terraform configuration files to deploy the project in a DigitalOcean Spaces bucket. The deployment takes plae in the continous-deployment Github Actions workflow.

To succesfully execute the deployment process, these credentials should be available in Github Actions Secrets:

- `TF_VAR_DO_TOKEN:` Digital Ocean API key
- `STATE_FILE:` Digital Ocean space bucket state file
- `SPACE_NAME:` Digital Ocean space bucket name
- `AWS_ACCESS_KEY_ID:` Digital Ocean space bucket key ID
- `AWS_SECRET_ACCESS_KEY:` Digital Ocean space bucket secret key
- `TERRAFORM_PRIVATEKEY:` ssh private key
- `TERRAFORM_PUBLICKEY:` ssh public key
- `MYSQL_PASSWORD:` MYSQL database password
- `MYSQL_USERNAME:` MYSQL database username
- `MYSQL_HOST:` MYSQL database hostname
- `MYSQL_PORT:` MYSQL database port number
- `MYSQL_DATABASE:` MYSQL database danme
- `DOCKER_USERNAME:` Dockerhub account's username to store docker images
- `DOCKER_PASSWORD:` Dockerhub account's password to store docker images