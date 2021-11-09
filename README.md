# mss-mongo-springboot-app
docker run -d -e MONGO_DB_USERNAME=devdb -e MONGO_DB_HOSTNAME= mongo -e MONGO_DB_PASSWORD=devdb123 -p 8080:8080 --name agunuapp --network mss-network  agunu2025/mss-mongodb-app:1
###########
docker volume ls
# How to create a volume
docker volume create -d <driver> <volumeName>
ex:
docker volume create -d local  mongobkp
#How to mount volume with docker container?
docker run -d -v <volumeName>:<containerPath> --network <networkName> <imageName>
ex:
        now network
docker run -d  --name mongo -e MONGO_INITDB_ROOT_USERNAME=devdb -e MONGO_INITDB_ROOT_PASSWORD=devdb123 mongo

docker run -d  -p 8080:8080 -e MONGO_DB_USERNAME=devdb -e MONGO_DB_HOSTNAME= mongo -e MONGO_DB_PASSWORD=devdb123 --name agunuapp agunu2025/mss-mongodb-app:1


        #The same network
docker run -d --name mongo -e MONGO_INITDB_ROOT_USERNAME=devdb -e MONGO_INITDB_ROOT_PASSWORD=devdb@123 --network mss-network mongo

docker run -d -e MONGO_DB_USERNAME=devdb -e MONGO_DB_HOSTNAME=mongo -e MONGO_DB_PASSWORD=devdb@123 -p 8080:8080 --name agunuapp --network mss-network agunu2025/mss-mongodb-app:1


docker run -d  --name mongo -v mongobkp:/data/db  --network agununetwork mongo
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
