# Course_Project

## Vision
This project demonastrates a two-component containerized application using Infrastructure as Code principles.

### Architecture

![Architecture](diagrams/architechture.png)

### Components

Component 1: Web Application (Node.js)
- Handles HTTP requests from users.
- Displays the current visitor count.
- Increments the visitor count on each request.

Component 2: Redis
- Stores the visitor counter.
- Updates the count when requested by the web application.
- Communicates with the web application using TCP.

### Communication Flow

Browser -> HTTP -> Web App
Web App -> TCP (Redis protocol) -> Redis
Redis -> Web Application -> Browser


## Proposal

This project will use lightweight container images for deployment.

- Web Application Base Image: `node:18-alpine`
- Redis Base Image: `redis:7-alpine`

The final deployment will be demonstrated on CloudLab using containerization.

## Build Process

I created a Dockerfile inside the app folder to containerize my Node.js application.
Here is what each line does:

- FROM node:18-alpine
    I chose this base image because it is a smaller version of Node.js, which makes the container lighter and faster to run.

- WORKDIR /app
    This sets the working directiory inside the container so all commands run in the app folder.

- COPY package*.json ./
    This copies the package files first so Docker can cache the dependencies and not reinstall them every time.

- RUN npm install
    This installs all the dependencies needed for the app like express and redis.

- COPY . .
  This copies the rest of the application code into the container.

- EXPOSE 3000
  This tells Docker that the app will run on port 3000.

- CMD ["node", "app.js"]
    This starts the Node.js application when the container runs.
I used docker-compose to build and run both the web container and the Redis container together.

## Networking

The containers communicate using Docker's default bridge network.
When I run docker-compose, Docker automatically puts both containers on the same netowork and assigns them IP addresses.
Instead of using IP addresses directly, I used the name "redis" in my code to connect to the Redis container. Docker automatically translates this name to the correct IP aaddress.
This makes it easier because I don't have to worry about IPs changing.

The communcation works like this:
1. The browser sends a request to the web container
2. The web container connects to Redis using TCP on port 6379
3. Redis updates the visitor count and sends it back.

This setup allows the containers to talk to each other internally without exposing Redis to the outside.
