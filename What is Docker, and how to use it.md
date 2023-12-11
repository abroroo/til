### WTF is Docker? 

Docker enables your app to run on any computer with the same configuration, for example same environment and service, meaning (same Node.js version, same database version, etc.) **So you can avoid:**

 ![, but it works on my computer problem](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRAKilXOwKaMrv205lA2YL8ALeY2xgQunfVCKZl-AeL2vg73Wu0kJuFBNWHIV9QdGcTqAQ&usqp=CAU)


Docker uses a concept of **image** which are like pre-packaged services (Node.js, MongoDB, Postgres, Ubuntu, etc.) ready to run in isolated containers. Think of them like npm packages in Node.js. See [docker hub](https://hub.docker.com/) for the collection of images available to use in docker containers  

#### Getting Started: 
1. Create a Dockerfile in your app's root directory. This text file instructs Docker how to build your application's image. Nameing _Dockerfile_ is required. 
  > A Dockerfile is a text file that contains instructions for building a Docker image. The Docker image is a self-contained package that includes everything needed to run       an application, including the application code, libraries, and dependencies. The Dockerfile ensures that your application is built the same way every time, regardless of the environment. This is important for reproducibility and debugging.
  Sample [Dockerfile](https://docs.docker.com/engine/reference/builder/)
   ```
    FROM node:18.19.0          #specifyes base image to use and its version
    
    WORKDIR /Users/abror/Documents/docker-example    #where the container should be created in your computer 
    
    COPY ./ ./                 #copies everything in the root of your app to the root of the container 
    
    RUN npm install            #specifies what to run after a container is created 
    
    CMD ["/bin/bash"]          #specifies the command to run when the container starts.

   ``` 

2. Then build the image with  `docker build -t <your_container_name>`
3. Run the container with `docker run -it <your_container_name>`  Use `-d` to run it in the background without opening a terminal.
4. Specify the port with `docker run -it -p <host_port>:<container_port> <your_container_name>`


That should be it!

**Other common commands:**

`docker ps` can see current containers

`docker exec -it containerId  bash` opens an interactive shell session inside the specified container, allowing you to execute commands and interact with the container's files and processes.

`docker stop containerId`  stops a running container

See all available commands in the [docs](https://docs.docker.com/engine/reference/commandline/cli/) 


     
