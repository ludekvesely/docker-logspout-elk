# Docker-compose.yml file with logspout and ELK stack

> Check out my my article: http://www.ludekvesely.cz/docker-a-logovani/

This docker-compose.yml file contains 4 services:

- [Logspout](https://hub.docker.com/r/gliderlabs/logspout/): Log router for Docker cantainers which attaches to all containers on a host and routes their logs to logstash
- [Logstash](https://hub.docker.com/_/logstash/): Tool that can be used to collect, process and forward log messages
- [Elasticsearch](https://hub.docker.com/_/elasticsearch/): Search server based on Lucene.
- [Kibana](https://hub.docker.com/_/kibana/): Data visualisation plugin for Elasticsearch.

### How to start this stack?

Just cd into directory with docker-compose.yml and type:

```
docker-compose up
```

You shoud see how is stack starting. Now open another terminal and run:

```
docker run --rm alpine echo This is my log message
```

Your message should appear first terminal:

```
logstash_1       | {
logstash_1       |          "@version" => "1",
logstash_1       |        "@timestamp" => "2016-04-30T08:23:24.934Z",
logstash_1       |              "type" => "docker",
logstash_1       |              "host" => "172.17.0.5",
logstash_1       |           "service" => "ab",
logstash_1       |     "containerName" => "romantic_jennings",
logstash_1       |           "message" => "This is my log message"
logstash_1       | }
```

This message shoud be also stored in Elasticsearch and visible in Kibana - visit https://localhost:5601, click on **Create** button and go to **Discover** tab.

![Choose index pattern in Kibana](http://www.ludekvesely.cz/content/images/2016/04/kibana-start-pattern.png)

Your log message should appear in Kibana:

![Kibana - discover](http://www.ludekvesely.cz/content/images/2016/04/kibana-discover.png)
