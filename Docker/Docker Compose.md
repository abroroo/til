### What is Docker Compose?

> Docker Compose is a tool for defining and running multi-container Docker applications. It lets you describe the services that make up your app in a [YAML](https://yaml.org/) file, and then provides a convenient way to start, stop, and scale them.

### In my own words: 
Basically, it's a file with [some-name].yaml extension in the root of your project, with which you can manage multiple docker containers. Instead of having to manage each container individually, you can define them all in one place and then manage them as a group.


### How to get started with Docker Compose
They have a very nice [tutorial](https://docs.docker.com/compose/gettingstarted/) on how to get started with docker compose. 

For Mac and Windows, it comes with the Docker app that you have installed on your computer. So all you need to do is to create a docker-compose.yaml file in the root of your project. 

Here's an example of a simple Compose file for a nextjs application with postgres database:

*# I've added comments to explain each option*
```
# Specifies the Docker Compose version used. This version is required for some features.

version: "3.8"  

# Defines the services that make up your application. Each service is
# like a standalone building block within your app.

services:

  # Defines a service named "frontend" This service runs your Next.js application.

  frontend:

    # Specifies the Docker image to use for the "frontend" service. In this case,
    # it will use the latest version of the official Next.js image.

    image: nextjs:latest

    # Maps the container port 3000 (where Next.js runs) to the host port 80.
    # This makes your application accessible at http://localhost:80 on your machine.

    ports:
      - "80:3000"

    # Mounts a volume named "appName" from the host directory "./appName" (your
    # local application code) to the container directory "/appName" (where Next.js
    # expects to find the application code). This allows your local changes
    # to be reflected in the running application.

    volumes:
      - ./appName:/appName

  # Defines a service named "db". This service runs your PostgreSQL database.

  db:
    # Specifies the Docker image to use for the "db" service. In this case,
    # it will use the latest version of the official PostgreSQL image.

    image: postgres:latest

    # Sets the environment variable "POSTGRES_PASSWORD" inside the
    # container to "password". This allows you to connect to the database
    # with this password.

    environment:
      POSTGRES_PASSWORD: password

    # Mounts a volume named "db-data" to the container directory
    # "/var/lib/postgresql/data". This is where the database stores its data,
    # ensuring it exists even if the container is stoped or deleted.

    volumes:
      - db-data:/var/lib/postgresql/data

# Defines the volumes used by the services. For volumes in here you define what you want to exist outside of individual containers, be perisistent no matter if container is running or deleted

volumes:

  # Defines a volume named "db-data". This volume will be used to store
  # the PostgreSQL database's data.

  db-data:




```
 **You can learn more about available options for Compose file in [here](https://docs.docker.com/compose/compose-file/03-compose-file/)**

Once you have a Compose file, you can use the following commands to manage your application:

`docker-compose up` : Starts all of the services defined in your Compose file.

`docker-compose down` : Stops all of the services defined in your Compose file.

`docker-compose ps` : Shows the status of all of the services defined in your Compose file.

