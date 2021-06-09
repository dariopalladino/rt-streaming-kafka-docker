# Real-time IoT Data Streaming with Kafka on Docker
This project is based on an experimental idea by [Dineshkarthik Raveendran](https://medium.com/@dineshkarthik.r?source=post_page-----e9fbee6ecc91--------------------------------)
You can use either a SensorApp like [Sensorstream IMU+GPS](https://play.google.com/store/apps/details?id=de.lorenz_fenster.sensorstreamgps&hl=en) or create a simple GeoLocation app with a kafka client that streams directly to your kafka server or through udp:// socket to your kafka producer server. Both ways work.

All components are dockerized and managed through docker-compose stack.

![Architecture](architecture.png)

> Kafka and Zookeper with two replications.
> Kafka producer exposed on local server to receive streaming from the smartphone
> Kafka Magic and Kafdrop to handle topics and partitions, with javascript query-like
> Logstash, Elasticsearch and Kibana for data visualization and dashboards

By default, the stack exposes the following ports:

- 5555: kafka producer UDP input
- 9093: Kafka port for host interaction
- 9200: Elasticsearch HTTP
- 9300: Elasticsearch TCP transport
- 5601: Kibana
- 8086: Kafka Magic
- 8085: Kafdrop

## Execution

```sh
$ docker-compose -f build/docker-compose.yml -p iot-project up --build -d
```
- the --build option is required to build the kafka-producer the first time, next time you can just use same command without --build option.

Then click `Switch Stream` button in Sensorstream IMU+GPS app to switch on the stream.

```sh
$ docker-compose -f build/docker-compose.yml down
```
- To shutdown the whole stack

## Querying the sensor data / Data Visualization

Open kibana in your browser using url [http://localhost:5601](http://localhost:5601)
- Click on the discover button on the left navigation bar.
- Kibana will prompt you to `Define index pattern` type `logstash-*` and press next
- Step 2 you will be asked to choose th `Time Filter field name` select `@timestamp` from the drop down and press `Create Index`
- Now go to discover section. You can see the data coming in from the android smartphone.
