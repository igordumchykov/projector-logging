# projector-logging
Sets up logging for MySQL slow query log using ELK stack and GrayLog

# Project Structure
- [config](./config): configuration files for elasticsearch, filebeat, kibana and logstash
- [data](./data): mongodb data for graylog
- [docker compose for ELK](./docker-compose-elk.yaml): docker compose file to test ELK stack
- [docker compose for GrayLog](./docker-compose-graylog.yaml): docker compose file to test GrayLog
- [logs](./logs): MySQL slow query logs

# Run
1. ELK stack
```shell
docker-compose --file ./docker-compose-elk.yaml up -d
```

Execute slow query in mysql:

Connect to mysql container and execute slow query:
```mysql
select sleep(5);
```
Go to `localhost:5600` to see logs in Kibana:
![alt_text](./docs/elk.png)

2. GrayLog
```shell
docker-compose --file ./docker-compose-graylog.yaml up -d
```

Execute slow query in mysql:

Connect to mysql container and execute slow query:
```mysql
select sleep(5);
```

Inside Graylog's web interface `localhost:9000`:

- Go to System -> Inputs.
- Select Beats from the drop-down list and click on Launch new input.
- Fill out the necessary details, like the bind address (0.0.0.0 to listen on all interfaces) and the port (e.g., 5044).
- Start the input. Filebeat should now be able to send logs to this input.
- 
![alt_text](./docs/graylog.png)
