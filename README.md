# Project Setup

First we need to create a .env file to provide critical values to the elasticsearch and kibana:

*.env*

```
# Password for the 'elastic' user (at least 6 characters)
ELASTIC_PASSWORD=<xxxxxx>

# Password for the 'kibana_system' user (at least 6 characters)
KIBANA_PASSWORD=<xxxxxx>

# Version of Elastic products
STACK_VERSION=8.6.1

# Set the cluster name
CLUSTER_NAME=docker-cluster

# Set to 'basic' or 'trial' to automatically start the 30-day trial
LICENSE=basic
#LICENSE=trial

# Port to expose Elasticsearch HTTP API to the host
ES_PORT=9200
#ES_PORT=127.0.0.1:9200

# Port to expose Kibana to the host
KIBANA_PORT=5601
#KIBANA_PORT=80

# Increase or decrease based on the available host memory (in bytes)
MEM_LIMIT=1073741824

# Project namespace (defaults to the current folder name if not set)
#COMPOSE_PROJECT_NAME=myproject

```

Starting the Project:
```
docker-compose up -d
```

This should download the required packages, build the images and setup the containers for you.
![image](https://user-images.githubusercontent.com/46488345/218675861-266184de-18c4-4350-ab70-04d2057a20de.png)

![image](https://user-images.githubusercontent.com/46488345/218676354-da1b843a-4772-4105-98dd-db89c0576063.png)

After the process is complete you can take a look at your running containers using the following command:
```
docker ps -a
```
![image](https://user-images.githubusercontent.com/46488345/218677063-cc3ca0c6-40f9-4d5d-88fc-5d48b4edfb6e.png)

