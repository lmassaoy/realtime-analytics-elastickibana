# [![kibana-dashboard-title.png](https://i.postimg.cc/Y0GPkdJJ/kibana-dashboard-title.png)](https://postimg.cc/zHN7FFDj)
This project brings multiple components to build and run a fast-data application, messaging broker, streaming service, indexed DB, and real-time analytics dashboard

You gonna need to build the image of the event-producer. To handle this, go to application's [repository](https://github.com/lmassaoy/valorant-matches-event-producer) and follow the steps to do it (JVM mode).

# Architecture
[![fastdata-architecture.png](https://i.postimg.cc/RhrhKF4D/fastdata-architecture.png)](https://postimg.cc/FdZhQhfy)

| Layer/Role | Component |
|-|-|
| Application | [Event Producer](https://github.com/lmassaoy/valorant-matches-event-producer) (Quarkus) |
| Messaging | Apache Kafka (1 broker / 3 partitions) |
| Streaming | Apache Nifi (Kafka to Elastic) |
| Database | Elasticsearch 7.9.1 (2 nodes) |
| Analytics/DataViz | Kibana 7.9.1 |

# Build'n'Run

## Docker Compose
Very straight forward, just run the command to start the containers
```
$ docker-compose -f devops/docker-compose.yml up -d
```
It takes a couple minutes to start everything  :)

Here are the URLs of the components:

**Event Producer**
- http://localhost:8080/health - health-check
- http://localhost:8080/metrics/application - metrics (prometheus model)

**Apache Kafka**
- http://localhost:9000/topic/matches - Kafdrop (Kafka Web UI) - topic "matches"

**Apache Nifi**
- http://localhost:8081/nifi/ - Nifi Web UI

**Elasticsearch**
- http://localhost:9200/_cat/nodes?v&pretty - Elasticsearch (check nodes)

**Kibana** (the last one in the starting phase)
- http://localhost:5601/ - Kibana


To turn the things off:
```
$ docker-compose -f devops/docker-compose.yml down -v
```

## Setup
### Apache Nifi
Import the xml template of the streaming processors (kafka-to-elastic) and start the processors.



### Kibana
Import the "json" file in the "**Saved Objects**" section. This will allow you to access the dashboard.

## Dashboard
For a better experience, turn the dark theme ON :)
