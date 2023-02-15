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


# REST API's of Elastic Search

Open the `http://localhost:5601`  on your dashboard it will redirect you to the login page
![image](https://user-images.githubusercontent.com/46488345/218734868-597c1eba-8385-4a0c-ace3-d93e6b3763e2.png)

Enter the username as `elastic` and password as the one that you have set in *.env* file

Import the required data into Elastic Search.

Go to Dev Tools:


### CRUD FOR INDEXES

#### 1. CREATE INDEX - 
``` PUT /my-test-index```

#### 2. GET INDEX - 
``` GET /my-test-index```

#### 3. DELETE INDEX -
``` DELETE /my-index-000001```

#### 4. UPDATE INDEX MAPPING -
```
PUT /my-index-000001/_mapping
{
  "properties": {
    "name": {
      "type": "keyword"
    }
  }
}
```

#### 5. Search for available indexes using
```
# get available indices in the system
GET /_cluster/state?filter_path=metadata.indices.*.stat*
```

![image](https://user-images.githubusercontent.com/46488345/218784836-8c09a20e-eaa5-4ee9-87fd-3c0336c1bfea.png)


#### 6. For schema of the index
```
# get schema of the index
GET /kibana_sample_data_flights/_mapping
```
![image](https://user-images.githubusercontent.com/46488345/218787355-4f568fb3-a474-4e71-9331-9a3561e1cf1b.png)



### CRUD fOR DOCUMENTS

#### 1. Get data from an index -
```
# get data in an index
GET /kibana_sample_data_flights/_search
```

#### 2. GET One Object in a index
```
Syntax:
GET /<INDEX>/_doc/<ID>
E.G:
GET /kibana_sample_data_flights/_doc/kQLZT4YBiJoNOUFqknsz
GET /kibana_sample_data_flights/_source/kQLZT4YBiJoNOUFqknsz
```
#### 3. Update Document in an index (partially updates the body)-
```
Syntax:
POST /<INDEX>/_update/<ID>
{
"doc": <body>
}

POST /kibana_sample_data_flights/_update/kQLZT4YBiJoNOUFqknsz
{
  "doc": {
    "DestCountry": "IN",
    "OriginWeather": "Hail",
    "OriginLocation": {
      "lat": "19.0991",
      "lon": "72.8744"
    }
  }
}
```

#### 4. DELETE One Object in an index
```
DELETE /kibana_sample_data_flights/_doc/kQLZT4YBiJoNOUFqknsz
```

### FILTERS:

```
GET /kibana_sample_data_flights/_search?sort=FlightTimeHour
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "DestCountry": "US"
          }
        },
        {
          "match": {
            "OriginCountry": "KR"
          }
        },
        {
          "range": {
            "FlightTimeMin": {
              "gte": 800,
              "lte": 1000
            }
          }
        }
      ],
      "filter": {
        "term": {
          "OriginWeather": "Sunny"
        }
      }
    }
  }
}
```






