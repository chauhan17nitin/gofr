# Observability

Now that you have created your server, lets see how GoFr by default manages observability in different ways:

## Logs

  When we run our server we see the following - logs for reading configs, database connection, requests, database queries, logs for missing configs etc.
  They contain information such as request's correlation ID, status codes, request time etc.

  Logs are generated only for events equal to or above the specified log level, by default GoFr logs at _INFO_ level.

  Log Level can be changed by setting the environment variable `LOG_LEVEL` value to _WARN,DEBUG,ERROR,NOTICE or FATAL_.

{% figure src="/quick-start-logs.png" alt="Pretty Printed Logs" /%}

  Logs are well-structured, they are of type JSON when exported to a file, such that they can be pushed to logging systems such as [Loki](https://grafana.com/oss/loki/), elastic search etc.

## Tracing

  GoFr adds traces by default for all the request and response,which allows you to export it to zipkin by adding the configs.
  It allows to monitor the request going through different parts of application like database, handler etc.

  To see the traces install zipkin image using the following docker command

  ### Setup

  ```bash
  docker run --name gofr-zipkin -p 2005:9411 -d openzipkin/zipkin:latest
  ```

  ### Configuration & Usage

  Add Tracer configs in `.env` file, your .env will be updated to

  ```bash
  APP_NAME=test-service
  HTTP_PORT=9000
  
  REDIS_HOST=localhost
  REDIS_PORT=6379
  
  DB_HOST=localhost
  DB_USER=root
  DB_PASSWORD=root123
  DB_NAME=test_db
  DB_PORT=3306
  
  TRACER_HOST=localhost
  TRACER_PORT=2005
  
  LOG_LEVEL=DEBUG
  ```

  Open [zipkin](http://localhost:2005/zipkin/) and search by TraceID (correlationID) to see the trace.

{% figure src="/quick-start-trace.png" alt="Pretty Printed Logs" /%}

