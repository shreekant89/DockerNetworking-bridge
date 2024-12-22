Dockerized Frontend and Backend Setup

This guide provides detailed instructions to set up and run a Dockerized .NET backend and an NGINX-based frontend that communicate seamlessly within the same Docker network.

Prerequisites

Docker installed on your system.

A .NET backend application.

A static frontend application (e.g., HTML + JavaScript).

Steps to Set Up

1. Create a User-Defined Docker Network

Create a custom Docker network to allow communication between the frontend and backend containers:

      cmd:- docker network create my-network


2. Create a .NET Backend Application
Create a new .NET Web API Project:(use bash or any other)

  dotnet new webapi -n BackendApp
  cd BackendApp

2.1 Build and Run Backend Container

Build and run the backend container:

    cmd:- docker build -t backend-app .
    cmd:- docker run -d --name backend --network my-network -p 5227:5227 backend-app


3.NGINX Configuration

Create an nginx.conf file to proxy requests to the backend:
    docker build -t frontend-app .
    docker run -d --name frontend --network my-network -p 8080:80 frontend-app

4. Test the Setup

  Open the frontend in your browser:

  http://localhost:8080

  The frontend should successfully fetch data from the backend and display:

  { "message": "Hello from the .NET Backend!" }

5. Troubleshooting

    1. Verify Containers are Running

    Run the following command to ensure both containers are running:

    docker ps

    Both frontend and backend containers should be listed.

    2. Verify Network Configuration

    Inspect the network to ensure both containers are connected:

    docker network inspect my-network

    Both frontend and backend should be listed under the Containers section.

    3. Test Backend Connectivity

    From within the frontend container, test connectivity to the backend:

    docker exec -it frontend curl http://backend:5227/weatherforecast

    You should receive the correct JSON response.

    4. Check Logs

    Frontend logs:

    docker logs frontend

    Backend logs:

    docker logs backend

