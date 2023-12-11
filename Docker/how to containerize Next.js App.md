### WTF is Docker? 

Docker enables your app to run on any computer with same configuration, for example same environment and service, meaning (same Node.js version, same databse version etc.) **So you can avoid:**

 ![, but it works on my computer problem](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRAKilXOwKaMrv205lA2YL8ALeY2xgQunfVCKZl-AeL2vg73Wu0kJuFBNWHIV9QdGcTqAQ&usqp=CAU)


Docker uses a concept of **image** which are services you can run on docker containers (Node.js, MongoDB, Postgres, Ubuntu etc.) , something like a npm packages for Node.js . See [docker hub](https://hub.docker.com/) for the collection of images available to use in docker containers  


*  In order to use docker u need to create a `Dockerfile` in the root directory of the app. Nameing _Dockerfile_ is required. 
  > A Dockerfile is a text file that contains instructions for building a Docker image. The Docker image is a self-contained package that includes everything needed to run       an application, including the application code, libraries, and dependencies. The Dockerfile ensures that your application is built the same way every time, regardless of the environment. This is important for reproducibility and debugging.

  Sample [Dockerfile](https://docs.docker.com/engine/reference/builder/)
   ```
    FROM node:18.19.0          #specifyes base image to use and it's version
    
    WORKDIR /Users/abror/Documents/docker-example    #where container should be created in your computer 
    
    COPY ./ ./                 #copies everything in the root of your app to the root of the container 
    
    RUN npm install            #specifies what to run after container is created 
    
    CMD ["/bin/bash"]          #specifies the command to run when the container starts.

   ``` 

