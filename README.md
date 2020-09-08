# [![dashboard-dark-title.png](https://i.postimg.cc/05VcRWpj/dashboard-dark-title.png)](https://postimg.cc/NLr1RxCv)
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
Import the xml template (setup/nifi/kafka-to-elastic.xml) of the streaming processors (kafka-to-elastic) and start the processors.

[![Screen-Shot-2020-09-08-at-02-21-36.png](https://i.postimg.cc/RZCx0njZ/Screen-Shot-2020-09-08-at-02-21-36.png)](https://postimg.cc/YhPsnjr5)

Drag the template to the middle of the screen

[![Screen-Shot-2020-09-08-at-02-21-57.png](https://i.postimg.cc/B6P009R5/Screen-Shot-2020-09-08-at-02-21-57.png)](https://postimg.cc/vgyjrjYD)

and a selection box will appear.

[![Screen-Shot-2020-09-08-at-02-22-13.png](https://i.postimg.cc/c4RdCWCX/Screen-Shot-2020-09-08-at-02-22-13.png)](https://postimg.cc/D8w9ptqX)

This is what you gonna have if did everything properly :)

[![Screen-Shot-2020-09-08-at-02-22-29.png](https://i.postimg.cc/hGfFLR4F/Screen-Shot-2020-09-08-at-02-22-29.png)](https://postimg.cc/Z9tDmgyj)

Just start and you're good to go!

### Kibana
Import the "json" file in the "[**Saved Objects**](http://localhost:5601/app/management/kibana/objects)" section. This will allow you to access the dashboard.

[![Screen-Shot-2020-09-08-at-02-24-06.png](https://i.postimg.cc/02sqL4nm/Screen-Shot-2020-09-08-at-02-24-06.png)](https://postimg.cc/MXd4BdhK)

Select the file

[![Screen-Shot-2020-09-08-at-02-24-35.png](https://i.postimg.cc/xT3SYPpZ/Screen-Shot-2020-09-08-at-02-24-35.png)](https://postimg.cc/QHCzJc3g)


## Dashboard
For a better experience, turn the dark theme ON.

To do this, access the [Advanced Settings](http://localhost:5601/app/management/kibana/settings) page and toggle it on.

[![Screen-Shot-2020-09-08-at-02-25-14.png](https://i.postimg.cc/ZqRmwycM/Screen-Shot-2020-09-08-at-02-25-14.png)](https://postimg.cc/21Pg6ygQ)

Now just look for the Dashboard name as "Matches" in the Kibana panel (in the left)

[![Screen-Shot-2020-09-08-at-02-26-34.png](https://i.postimg.cc/C5yVMrV3/Screen-Shot-2020-09-08-at-02-26-34.png)](https://postimg.cc/JDQFPq0x)

This is your prize :) enjoy, explore, go beyond!

[![Screen-Shot-2020-09-08-at-02-27-31.png](https://i.postimg.cc/XY2SBYbc/Screen-Shot-2020-09-08-at-02-27-31.png)](https://postimg.cc/18NYLP4f)

[![Screen-Shot-2020-09-08-at-02-27-49.png](https://i.postimg.cc/0N3TZXrz/Screen-Shot-2020-09-08-at-02-27-49.png)](https://postimg.cc/wtX4jVXz)

[![Screen-Shot-2020-09-08-at-02-28-06.png](https://i.postimg.cc/Xq6T6Zf3/Screen-Shot-2020-09-08-at-02-28-06.png)](https://postimg.cc/S2VZWx1t)
