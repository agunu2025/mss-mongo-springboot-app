# mss-mongo-springboot-app
docker run -d -e MONGO_DB_USERNAME=devdb -e MONGO_DB_HOSTNAME=mongo -e MONGO_DB_PASSWORD=devdb@123 -p 8080:8080 --name agunuapp --network mss-network agunu2025/mss-mongodb-app:1

#What is network ?
#Group of servers will be connected to each other in a specific network. If Servers are in same network each one can talk to another server.
Docker network
#If One Container has to talk to another Container in Docker. Both has to created undersame docker network.

#If Containers are in two different networks. They can't accees each other.
docker run -d -p <hostPort>:<containerPort> --name <containerName> <imageName>

#In which docker network the container will be created if we don't mention network name while creating a container ?
#Containers will be created in a default bridge network.If we don't mention network name while creating a container.
#How to list networks in docker?
docker network ls

#Docker will have 3 networks by default.
bridge(default)
host
none/null
docker run -d -p 8080:8080 --name javabox agunu2025/mss-mongodb-app:1
docker run -d --name mysqbox -e MYSQL_ROOT_PASSWORD=devops@2019  mysql

#If containers are created in a default bridge network. Communcation will happen only with IP Address of container. Communcation will not happen using containerName(hostName).
#We should code the connectivity based on the IP. Since IP address of conainers will be dynamic.IP will keep changing.
# How to create a custom bridge network ?

# Create Network
docker network create -d <driver> <networkName>
Ex:
docker network create -d bridge mss-network

# Inspect network
docker network inspect <networkNameOrId>

# Remove unused networks
docker network prune

#Remove One or More Cotnainers
docker network rm <networkNameOrId>
docker run -d -p 8080:8080 --name tomcatcotnainer --network mss-network agunu2025/mss-mongodb-app:1

#Create another container in same network and try to ping with name & IP from above container.
docker run -d -p 8080:8080 --name dbcontainer --network mss-network mongo

#If containers are created in custom bridge network. Each container can access other using containerName/ContainerIP.
#Docker Host Network.

#If we create contaienrs in host network. Container will not have IP Address. Container will be created in a system network.
#But we can't create more than one cotnainer with same container port in host network.
Docker none/null network

#If we create contaienrs in none/null network. Container will not have IP Address.We can't  accees these contianers from out side or from any other cotnainer.

#########################################################
#1) Create docker network using below commond(If it's not created already)
docker network create  -d bridge flipkartnetwork
#2) Create Spring Application Container in above network & which will talk to mongo data base container
docker run -d -p 8080:8080 --name agunuapp --network mss-network  agunu2025/mss-mongodb-app:1
#3) Create a mongo contianer with out volume in above network
docker run -d --name mongo --network mss-network mongo



docker volume ls
# How to create a volume
docker volume create -d <driver> <volumeName>
ex:
docker volume create -d local  mongobkp
#How to mount volume with docker container?
docker run -d -v <volumeName>:<containerPath> --network <networkName> <imageName>
ex:
      Diff network
docker run -d  --name mongo -e MONGO_INITDB_ROOT_USERNAME=devdb -e MONGO_INITDB_ROOT_PASSWORD=devdb123 mongo

docker run -d  -p 8080:8080 -e MONGO_DB_USERNAME=devdb -e MONGO_DB_HOSTNAME= mongo -e MONGO_DB_PASSWORD=devdb123 --name agunuapp agunu2025/mss-mongodb-app:1


  #The same network
docker run -d --name mongo -e MONGO_INITDB_ROOT_USERNAME=devdb -e MONGO_INITDB_ROOT_PASSWORD=devdb@123 --network mss-network mongo

docker run -d -e MONGO_DB_USERNAME=devdb -e MONGO_DB_HOSTNAME=mongo -e MONGO_DB_PASSWORD=devdb@123 -p 8080:8080 --name agunuapp --network mss-network agunu2025/mss-mongodb-app:1


#How to list volumes?
docker volume ls
# How to create a volume
docker volume create -d <driver> <volumeName>
docker run -d  --name mongo -v mongobkp:/data/db  --network agununetwork mongo
docker volume create -d local  mongobkp
docker run -d  --name mongo -v mongobkp:/data/db  --network agununetwork mongo

#Bind Mounts
#When we use bind mount , a file or directory on the host machine is mounted into a container. The directory is referenced by it's full or relative path.
#Bind mounts will have limited functionality compared to volumes.
mkdir my-db-bkp
docker run -d --name mongo -e MONGO_INITDB_ROOT_USERNAME=devdb -v ~/my-db-bkp:/data/db -e MONGO_INITDB_ROOT_PASSWORD=devdb@123 --network mss-network mongo
#############################
#Volumes are prefered way for persisting data generated and used by docker containers.While bind mounts are dependent on the directory strucute of the host system.
docker volume create -d <driver> <volumeName>
docker volume create -d local  mongobkp
docker run -d --name mongo -e MONGO_INITDB_ROOT_USERNAME=devdb -v mongobkp:/data/db -e MONGO_INITDB_ROOT_PASSWORD=devdb@123 --network mss-network mongo


# Install Rex ray EBS Volume driver plugin
rexray.readthedocs.io/en/stable/user-guide/schedulers/docker/plug-ins/aws/

#volume
#Install Rex ray EBS Volume driver plugin
rexray.readthedocs.io/en/stable/user-guide/schedulers/docker/plug-ins/aws/

docker plugin install rexray/ebs EBS_ACCESSKEY=<awsAccessKey> EBS_SECRETKEY=<aws_secretkey>
EX:
docker plugin install rexray/ebs EBS_ACCESSKEY=AKIAUQ6YGCGHCGI4WLMI EBS_SECRETKEY=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
docker volume create -d rexray/ebs mongodbbkp


docker plugin install rexray/s3fs \  S3FS_ACCESSKEY=AKIAJIV3V2OLTBE5O6HQ \  S3FS_SECRETKEY=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
docker volume create -d rexray/s3fs mongoebsbkp
docker plugin install --alias rexray/s3fs --grant-all-permissions \
  rexray/s3fs:0.11.3 \
  S3FS_ACCESSKEY=AKIAJIV3V2OLTBE5O6HQ \
  S3FS_SECRETKEY=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 \
  S3FS_REGION=us-west-2 \
  REXRAY_LOGLEVEL=debug

 docker plugin install rexray/s3fss \
  S3FS_ACCESSKEY=AKIAJIV3V2OLTBE5O6HQ \
  S3FS_SECRETKEY=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

AWSAccessKeyId=AKIAJIV3V2OLTBE5O6HQ
AWSSecretKey=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
                                                  #Volume Mapping While creating a container
 docker run -d -p 8080:8080 --name agunuapp --network agununetwork  agunuworld/spring-boot-mongo:5
docker run -d  --name mongo -v mongoebsbkp:/data/db  --network agununetwork mongo
docker run -d  --name mongo -v mongoebsbkp:/data/db  --network flipkartnetwork mongo
                                                     #Docker Compose:
                                                       #It's tool for defining and runing multicontainer applications.It's a yml file.
                                                         #With Out Compose:
                                                           #We have to run long docker run commands to deploy multi continer applications.
docker volume create -d <driver> <volumeName>
docker volume create -d local mongobackup
docker network create -d <driver> <networkNAme>
docker network create -d bridge springappnetwork
docker run -d -p 8080:8080 --name springcontaienr --network springappnetwork agunu2025/mss-mongodb-app:1
docker run -d --name mongo --network springappnetwork -v mongobackup:/data/db mongo
