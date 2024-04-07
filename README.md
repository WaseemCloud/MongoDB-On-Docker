# MongoDB-On-Docker 🐳 📦
-------------------

![kisspng-docker-application-software-software-deployment-mi-docker-5ba331e62a2ce0 4850087515374217981728-removebg-preview](https://github.com/WaseemCloud/Dynamic-web-page---Docker/assets/157589909/7ad105da-5471-499e-9e21-e8bd93247787)


In this tutorial, I will be demonstrating how to build two containers. One for the MongoDB database, and the second for building Mongo-Express, which is the GUI version to facilate accessing the MongoDB.

-------------------

-------------------
# 1) Pulling MongoDB Docker image:
-------------------

- let's pull the image of MongoDB from DockerHub:

      docker pull mongo

-------------------
# 2) Pulling MongoDB-Express Docker image:
-------------------

- let's also pull the image of MongoDB-Express from DockerHub:

      docker pull mongo-express

-------------------
# 3) Verify that both images have been successfully pulled:
-------------------

    docker images


![image](https://github.com/WaseemCloud/MongoDB-Docker/assets/157589909/da6b8338-8d59-421a-8a7f-a26221605ce8)



-------------------
# 4) Creating Docker Network:
-------------------

- Before running these two containers, we need to create a Docker Network. This is the network where our containers will be laying in. Hence, it will allow the communication between all the containers that are residing in this network using the container name.

      docker network create mongo-network


- to verify that the network has been created:

      docker network ls

![image](https://github.com/WaseemCloud/MongoDB-Docker/assets/157589909/2250131b-fabf-4a73-8a0c-e35a56c97255)

- This command displays all the docker netwroks that are available. Including the default networks that are created by having Docker installed.


-------------------
# 5) Run MongoDB Container:
-------------------

    docker run -d -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password --name mongo --network mongo-network mongo

- Instead of using only run command in a single line, you can make the command more readable by using " \ " at the end of each entry.

- we are specifying our listening port to be "27017" for both the container and our machine.

- We are also specifying the network where our contanier will be laying in using "-net".

- We are renaming our container "mongoDB".

- "-e" is used to pass the environmental variables that are needed to be configured at the DB startup.

 - we are instructing to run these commands from the container image that we have "mongo".

-------------------
# 6) Run MongoDB-Express Container:
-------------------

    docker run -d -p 8081:8081 -e ME_CONFIG_MONGODB_SERVER=mongo -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=password --name mongo-express --network mongo-network mongo-express


- We are specifying that MongoExpress container should be connected to our MongoDB container "ME_CONFIG_MONGODB_SERVER=mongo".

- You may verify the logs in the created container:

      docker logs mongo-express

- "mongo-express": is the name of the container that you wish to view its logs.


-------------------
# 7) Verify that both containers are created:
-------------------

    docker ps -a

![image](https://github.com/WaseemCloud/MongoDB-Docker/assets/157589909/6b9b0b59-5695-48c2-9261-83a29d66f16c)

-------------------
# 8) Connect to MongoDB Express:
-------------------

- You should be able to connect to your MongoDB-Express by accessing the following URL:
  http://localhost:8081/

  ![image](https://github.com/WaseemCloud/MongoDB-Docker/assets/157589909/955834b6-35de-4a70-a6a3-9bb3bd145ec3)
  



-------------------
# Stopping the containers:
-------------------

- To stop containers, you can perform the following commands:

Container "mongo":

      docker stop mongo

Container "mongo-express":

      docker stop mongo-express

- Instead, you may stop both containers in one command:

      docker stop mongo mongo-express


-------------------
# Deleting the containers:
-------------------

- To delete both your containers:

  Container "mongo":

      docker rm mongo

Container "mongo-express":

      docker rm mongo-express

- Instead, you may delete both containers in one command:

      docker rm mongo mongo-express

-------------------
# Deleting container images:
-------------------

- To delete both your container images:

  Container "mongo":

      docker rmi mongo

Container "mongo-express":

      docker rmi mongo-express

- Instead, you may delete both container images in one command:

      docker rmi mongo mongo-express

-------------------
# Deleting Docker Network:
-------------------

    docker network rm mongo-network

    
