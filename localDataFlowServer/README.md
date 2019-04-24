# Getting Started - Local
> Refers: http://docs.spring.io/spring-cloud-dataflow/docs/2.0.2.RELEASE/reference/htmlsingle/#getting-started-local

There are 3 ways to start the data flow local server:

1. Using docker-compose to start data flow servers all in one
2. Download the OOTB JARs to start data flow servers manually one by one
3. Build the JARs yourself, then start data flow servers manually one by one

## Prerequisites
* Java8
* port: 9393 (`dataflow-server`)
* port: 9300 (`http-source-rabbit` app)
* port: 5672 (RabbitMQ)
* port: 15672 (RabbitMQ management)

## How to start data flow server
### Using docker compose
1. Install docker-compose: [https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/)
2. Start docker-compose:
```
sh start-docker-compose.sh
```
### Using JARs
#### Build/Download JARs
Download OOTB jars directly, or build jars yourself
> Refers: http://docs.spring.io/spring-cloud-dataflow/docs/2.0.2.RELEASE/reference/htmlsingle/#getting-started-local-deploying-streams-spring-cloud-dataflow

1. Download OOTB jars:
```
wget https://repo.spring.io/release/org/springframework/cloud/spring-cloud-dataflow-server/2.0.2.RELEASE/spring-cloud-dataflow-server-2.0.2.RELEASE.jar
wget https://repo.spring.io/release/org/springframework/cloud/spring-cloud-dataflow-shell/2.0.2.RELEASE/spring-cloud-dataflow-shell-2.0.2.RELEASE.jar
wget https://repo.spring.io/release/org/springframework/cloud/spring-cloud-skipper-server/2.0.1.RELEASE/spring-cloud-skipper-server-2.0.1.RELEASE.jar
wget https://repo.spring.io/release/org/springframework/cloud/spring-cloud-skipper-shell/2.0.1.RELEASE/spring-cloud-skipper-shell-2.0.1.RELEASE.jar
```

2. Build skipper JARs:
```
git clone git clone git@github.com:spring-cloud/spring-cloud-skipper.git
cd spring-cloud-skipper
git checkout 2.0.x
./mvnw clean install
```
Wait until build successfully:
```
[INFO] ------------------------------------------------------------------------
[INFO] Reactor Summary for Spring Cloud Skipper 2.0.2.BUILD-SNAPSHOT:
[INFO] 
[INFO] Spring Cloud Skipper ............................... SUCCESS [01:40 min]
[INFO] Spring Cloud Skipper :: Skipper .................... SUCCESS [ 31.595 s]
[INFO] Spring Cloud Skipper :: Server Core ................ SUCCESS [08:25 min]
[INFO] Spring Cloud Skipper :: Kubernetes Platform ........ SUCCESS [  7.773 s]
[INFO] Spring Cloud Skipper :: CloudFoundry Platform ...... SUCCESS [ 12.102 s]
[INFO] Spring Cloud Skipper :: Autoconfigure .............. SUCCESS [  7.756 s]
[INFO] Spring Cloud Skipper :: Server ..................... SUCCESS [  9.580 s]
[INFO] Spring Cloud Skipper :: Client ..................... SUCCESS [  7.172 s]
[INFO] Spring Cloud Skipper :: Shell Commands ............. SUCCESS [ 20.973 s]
[INFO] Spring Cloud Skipper :: Shell ...................... SUCCESS [  1.780 s]
[INFO] Spring Cloud Skipper :: Docs ....................... SUCCESS [  0.218 s]
[INFO] Spring Cloud Skipper :: Dependencies ............... SUCCESS [  0.052 s]
[INFO] Spring Cloud Starter :: Skipper Server ............. SUCCESS [  1.116 s]
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  11:47 min
[INFO] Finished at: 2019-04-24T10:57:57+08:00
[INFO] ------------------------------------------------------------------------
```
JARs location:
```
./spring-cloud-skipper/spring-cloud-skipper-server/target/spring-cloud-skipper-server-2.0.2.BUILD-SNAPSHOT.jar
./spring-cloud-skipper/spring-cloud-skipper-shell/target/spring-cloud-skipper-shell-2.0.2.BUILD-SNAPSHOT.jar
```
3. Build dataflow JARs:
```
git clone git@github.com:spring-cloud/spring-cloud-dataflow.git
cd spring-cloud-dataflow
git checkout 2.0.x
./mvnw clean install
```
Wait until build successfully:
```
[INFO] Reactor Summary for spring-cloud-dataflow-parent 2.0.2.BUILD-SNAPSHOT:
[INFO] 
[INFO] spring-cloud-dataflow-parent ....................... SUCCESS [  2.304 s]
[INFO] spring-cloud-dataflow-configuration-metadata ....... SUCCESS [  5.593 s]
[INFO] spring-cloud-dataflow-core ......................... SUCCESS [  7.922 s]
[INFO] spring-cloud-dataflow-rest-resource ................ SUCCESS [ 15.487 s]
[INFO] spring-cloud-dataflow-audit ........................ SUCCESS [  5.617 s]
[INFO] spring-cloud-dataflow-registry ..................... SUCCESS [  6.173 s]
[INFO] spring-cloud-dataflow-completion ................... SUCCESS [  9.278 s]
[INFO] spring-cloud-dataflow-server-core .................. SUCCESS [04:34 min]
[INFO] spring-cloud-dataflow-platform-kubernetes .......... SUCCESS [ 10.147 s]
[INFO] spring-cloud-dataflow-platform-cloudfoundry ........ SUCCESS [ 11.976 s]
[INFO] spring-cloud-dataflow-autoconfigure ................ SUCCESS [ 42.144 s]
[INFO] spring-cloud-starter-dataflow-server ............... SUCCESS [ 50.119 s]
[INFO] Spring Cloud Data Flow Server ...................... SUCCESS [ 41.660 s]
[INFO] spring-cloud-dataflow-rest-client .................. SUCCESS [ 11.019 s]
[INFO] spring-cloud-dataflow-shell-core ................... SUCCESS [01:10 min]
[INFO] spring-cloud-dataflow-shell ........................ SUCCESS [  1.984 s]
[INFO] Spring Cloud Data Flow Docs for Classic mode ....... SUCCESS [06:15 min]
[INFO] Spring Cloud Data Flow Docs ........................ SUCCESS [  0.154 s]
[INFO] spring-cloud-dataflow-dependencies ................. SUCCESS [  0.034 s]
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  15:46 min
[INFO] Finished at: 2019-04-24T10:38:53+08:00
[INFO] ------------------------------------------------------------------------
```
JARs location:
```
./spring-cloud-dataflow/spring-cloud-dataflow-server/target/spring-cloud-dataflow-server-2.0.2.BUILD-SNAPSHOT.jar
./spring-cloud-dataflow/spring-cloud-dataflow-shell/target/spring-cloud-dataflow-shell-2.0.2.BUILD-SNAPSHOT.jar
```
#### Start JARs
```
java -jar spring-cloud-skipper-server-2.0.1.RELEASE.jar
java -jar spring-cloud-dataflow-server-2.0.2.RELEASE.jar
java -jar spring-cloud-dataflow-shell-2.0.2.RELEASE.jar
```
Or
```
java -jar spring-cloud-skipper-server-2.0.2.BUILD-SNAPSHOT.jar
java -jar spring-cloud-dataflow-server-2.0.2.BUILD-SNAPSHOT.jar
java -jar spring-cloud-dataflow-shell-2.0.2.BUILD-SNAPSHOT.jar
```
If successful, you will see:
```
Successfully targeted http://localhost:9393/
dataflow:>
```
##### Trouble Shooting
1. If `skipper-server` and `dataflow-server` are not running on the same host:

Need setting `skipper-server`'s host and port when starting `dataflow-server`: 
```
java -jar spring-cloud-dataflow-server-2.0.2.BUILD-SNAPSHOT.jar --spring.cloud.skipper.client.serverUri=http://<skipper-server host>:<skipper-server port>/api
```
Or
```
java -jar spring-cloud-dataflow-server-2.0.2.RELEASE.jar --spring.cloud.skipper.client.serverUri=http://<skipper-server host>:<skipper-server port>/api
```
2. If `dataflow-server` and `dataflow-shell` are not running on the same host:
You will see:
```
server-unknown:>
```
Need set `dataflow-server` host and port in `dataflow-shell`:
```
dataflow config server http://<dataflow-server host>
```
If successful you will see:
```
Successfully targeted http://<dataflow-server host>
dataflow:>
```
## Deploying streams in data flow server
### Prerequisites
    * RabbitMQ be running on the same machine as Skipper and the Spring Cloud Data Flow server and shell.
#### Start RabbitMQ via docker
```
docker pull rabbitmq:management
docker run -d --hostname my-rabbit --name rabbitmq -p 15672:15672 -p 5672:5672 -p 25672:25672 -p 61613:61613 -p 1883:1883 rabbitmq:management
```
View rabbitmq logs:
```
docker logs rabbitmq
```
Visit rabbitmq management: [http://127.0.0.1:15672/](http://127.0.0.1:15672/)

Default Username/password: `guest/guest`

##### Trouble Shooting
Start RabbitMQ docker container with custom username/password:
```
docker run -d --hostname my-rabbit --name rabbitmq -e RABBITMQ_DEFAULT_USER=admin -e RABBITMQ_DEFAULT_PASS=admin -p 15672:15672 -p 5672:5672 -p 25672:25672 -p 61613:61613 -p 1883:1883 rabbitmq:management
```
Then management isername/password should be: `admin/admin`
### Using docker-compose
Visit: [http://localhost:9393/dashboard](http://localhost:9393/dashboard)

Then follow the Spring Cloud Data Flow Reference Guide.
> Refers: http://docs.spring.io/spring-cloud-dataflow/docs/2.0.2.RELEASE/reference/htmlsingle/#getting-started-local-deploying-spring-cloud-dataflow-docker-deploy-stream
### Using JARs
#### Register a stream app
> Refers: http://docs.spring.io/spring-cloud-dataflow/docs/2.0.2.RELEASE/reference/htmlsingle/#spring-cloud-dataflow-register-stream-apps

For example, register a `http-source-rabbit`, `log-sink-rabbit`
```
dataflow:>app register --name http --type source --uri maven://org.springframework.cloud.stream.app:http-source-rabbit:1.2.0.RELEASE
dataflow:>app register --name log --type sink --uri maven://org.springframework.cloud.stream.app:log-sink-rabbit:1.1.0.RELEASE
```
If successful, you will see:
```
Successfully registered application 'source:http'
Successfully registered application 'sink:log'
```
List all exist apps:
```
dataflow:>app list
```
Output:
```
╔═══╤══════╤═════════╤════╤════╗
║app│source│processor│sink│task║
╠═══╪══════╪═════════╪════╪════╣
║   │http  │         │log │    ║
╚═══╧══════╧═════════╧════╧════╝
```
Then the `http-source-rabbit` app has been successfully created at [http://localhost:9000](http://localhost:9000)
#### Create a stream
1. For example, create a stream with `http-source-rabbit` and `log-sink-rabbit` apps

```
dataflow:>stream create --name httptest --definition "http --server.port=9000 | log" --deploy
```
If successful, you will see:
```
Created new stream 'httptest'
Deployment request has been sent
```
List all the streams:

```
dataflow:>stream list
```
Output:
```
╔═══════════╤═════════════════════════════╤═════════════════════════════════════════╗
║Stream Name│      Stream Definition      │                 Status                  ║
╠═══════════╪═════════════════════════════╪═════════════════════════════════════════╣
║httptest   │http --server.port=9000 | log│The stream has been successfully deployed║
╚═══════════╧═════════════════════════════╧═════════════════════════════════════════╝
```
2. Find the `log-sink-rabbit` log files location from `skipper-server` instance output log:
```
...
2019-04-24 13:38:20.827  INFO 28553 --- [nio-7577-exec-1] o.s.s.s.DefaultStateMachineService       : Acquiring machine with id httptest
...
2019-04-24 13:38:21.607  INFO 28553 --- [eTaskExecutor-3] o.s.c.d.spi.local.LocalAppDeployer       : Deploying app with deploymentId httptest.http-v1 instance 0.
   Logs will be in /tmp/spring-cloud-deployer-5882466766166656636/httptest-1556084301558/httptest.http-v1
...
2019-04-24 13:38:21.723  INFO 28553 --- [eTaskExecutor-3] o.s.c.d.spi.local.LocalAppDeployer       : Deploying app with deploymentId httptest.log-v1 instance 0.
   Logs will be in /tmp/spring-cloud-deployer-5882466766166656636/httptest-1556084301609/httptest.log-v1
...
```

3. View the log:
```
view /tmp/spring-cloud-deployer-5882466766166656636/httptest-1556084301609/httptest.log-v1/stdout_0.log 
```
If Stream connect to RabbitMQ succefully, you will see the log:
```
o.s.c.s.a.l.s.r.LogSinkRabbitApplication : Started LogSinkRabbitApplication in 13.392 seconds (JVM running for 14.366)
```
##### Trouble Shooting
1. If the log output is as follows:
```
o.s.a.r.l.SimpleMessageListenerContainer : Consumer raised exception, processing can restart if the connection factory supports it. Exception summary: org.springframework.amqp.AmqpConnectException: java.net.ConnectException: Connection refused (Connection refused)
```
Means RabbitMQ is not running or stream cannot connect to the default RabbitMQ host and port: `localhost:5672`

1. If the log output is as follows:
```
org.springframework.amqp.rabbit.listener.exception.FatalListenerStartupException: Authentication failure
```
Means stream cannot connect to RabbitMQ using default username/password: `guest/guest`
#### Post test data to stream
```
dataflow:>http post --target http://localhost:9000 --data "hello world"
```
If successful you will see:
```
> POST (text/plain) http://localhost:9000 hello world
> 202 ACCEPTED
```
Check results in `log-sink-rabbit` log files:
```
view /tmp/spring-cloud-deployer-5882466766166656636/httptest-1556084301609/httptest.log-v1/stdout_0.log
```
You will see:
```
2019-04-24 14:35:55.214  INFO 26057 --- [http.httptest-1] log-sink                                 : hello world
```
#### Upgrade exist app versions
TBD
#### Rolling back exist app versions
TBD