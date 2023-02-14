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



