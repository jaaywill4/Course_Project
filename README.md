# Course_Project

## Vision
THis project demonastrates a two-component containerized application using infrastructure as code principles.

### Architecture

![Architecture](diagrams/architechture.png)

### Components

Component 1: Web APplication (Node.js)
- Handles HTTP requests from useers.
- Displays and increments visitor count.

Component 2: Redis
- Stores and updates visitor counter.
- Communicates with the web application using TCP.

### Communication Flow

Browser -> HTTP -> Web App
Web App -> TCP (Redis protocol) -> Redis


## PRoposal

This project will use lightweight container images for deployment.

- Web Application Base Image: `node:18-alpine`
- Redis Base Image: `redis:7-alpine`

The final deployment will be demonstrated on CloudLab using containerization.
