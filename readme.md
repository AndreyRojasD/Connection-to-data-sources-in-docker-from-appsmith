# Previous requirements
- Docker
- Ngrok
- Docker install follow this link:https://docs.docker.com/engine/install/
- Ngrok install follow this link:https://ngrok.com/

# Connect Mongodb container with Appsmith
- Create a mongoDB docker-compose.yml
```

version: '3.1'
services:
  mongo:
    image: mongo:latest
    restart: always
    container_name: appsmithMongo
    hostname: host-appsmith-mongo
    environment:
      MONGO_INITDB_ROOT_USERNAME: root
      MONGO_INITDB_ROOT_PASSWORD: root
    ports:
      - "27017:27017"
```
- Run the docker container
- 
- Open an ngrok terminal and run the following command
`
 ngrok tcp mongoport
`
- Connect a new DataSource in Appsmith from MongoDB
- Get your mongo URI and put it on Appsmith's connection to mongo
- Press the test button to make sure of a correct connection

# Connect MySql container with appsmith
- Create a MySql docker-compose.yml: 
```
version: '3.3'
services:
  db:
    image: mysql:5.7
    restart: always
    environment:
      MYSQL_DATABASE: 'db'
      # So you don't have to use root, but you can if you like
      MYSQL_USER: 'user'
      # You can use whatever password you like
      MYSQL_PASSWORD: 'password'
      # Password for root access
      MYSQL_ROOT_PASSWORD: 'password'
    ports:
      # <Port exposed> : < MySQL Port running inside container>
      - '3306:3306'
    expose:
      # Opens port 3306 on the container
      - '3306'
      # Where our data will be persisted
    volumes:
      - my-db:/var/lib/mysql
# Names our volume
volumes:
  my-db:
```
- Run the docker container
- Open an ngrok terminal and run the following command
`
ngrok tcp 3306
`
- Connect a new DataSource in Appsmith from mysql
- Host and port are given by ngrok
- The username and password is found in the docker-compose file
- Press the test button to make sure of a correct connection

# Connect Postgress container with Appsmith
- Create a Postggress docker-compose.yml:
```
version: '3'
services:
  postgres:
          image: 'postgres:12'
          restart: always
          volumes:
          - './postgres_data:/var/lib/postgresql/data'
          environment:
          - POSTGRES_PASSWORD=secure_pass_here
          ports:
          - '5432:5432'
```
- Open an ngrok terminal and run the following command
`
ngrok tcp 5432
`
-Connect a new DataSource in Appsmith from Postgresql
- Host and port are given by ngrok
- Data base name
`
postgres
`
- User
`
postgres
`
- Password
`
secure_pass_here
`
- Press the test button to make sure of a correct connection

# Connect REDIS container with Appsmith

- Create a Redis docker-compose.yml:
```
version: '2'

services:
  redis:
    image: docker.io/bitnami/redis:7.0
    environment:
    #To use a specific password use this:- REDIS_PASSWORD=password123
      - ALLOW_EMPTY_PASSWORD=yes
      - REDIS_DISABLE_COMMANDS=FLUSHDB,FLUSHALL
    ports:
      - '6379:6379'
    volumes:
      - 'redis_data:/bitnami/redis/data'

volumes:
  redis_data:
    driver: local
```
- Open an ngrok terminal and run the following command
`
ngrok tcp 6379
`
- Connect a new DataSource in Appsmith from Redis 
- Host and port are given by ngrok
- Database Number in ` 0 `
- Press the test button to make sure of a correct connection

# Connect ElasticSearch container with Appsmith
- Create a ElasticSearch docker-compose.yml:
```
version: "3.0"
services:
  elasticsearch:
    container_name: es-container
    image: docker.elastic.co/elasticsearch/elasticsearch:7.11.0
    environment:
      - xpack.security.enabled=false
      - "discovery.type=single-node"
    networks:
      - es-net
    ports:
      - 9200:9200
  kibana:
    container_name: kb-container
    image: docker.elastic.co/kibana/kibana:7.11.0
    environment:
      - ELASTICSEARCH_HOSTS=http://es-container:9200
    networks:
      - es-net
    depends_on:
      - elasticsearch
    ports:
      - 5601:5601
networks:
  es-net:
    driver: bridge
```
` Note: This installation may take a long time. `
- Open an ngrok terminal the following command
` ngrok http 9200 `
- Connect a new DataSource in Appsmith from ElasticSearch
- Host given by ngrok
- The port for the connection is ` 443 `
- Press the test button to make sure of a correct connection

# Connect SqlServer container with Appsmith

- Create SqlServe docker-compose.yml
```
version: '3.9'
services:
  mssql:
    image: mcr.microsoft.com/mssql/server:2017-CU31-ubuntu-18.04
    ports:
      - 1433:1433
    volumes:
      - ~/apps/mssql/data:/var/lib/mssqlql/data
    environment:
      - ACCEPT_EULA=Y
      - SA_PASSWORD=mssql1Ipw
```
- Open an ngrok terminal the following command
` ngrok tcp 1433 `
- Connect a new DataSource in Appsmith from SqlServer
- Host and port are given by ngrok
- default database name: ` master `
- User Name: `sa`
- Password: ` mssql1Ipw `
- Press the test button to make sure of a correct connection
# Connect SMTP container with Appsmith
- Create SMTP docker-compose.yml
```
version: '3'
services:
  mail:
    image: bytemark/smtp
    restart: always
    ports:
     - "25:25"
    environment:
      RELAY_HOST: smtp.gmail.com
      RELAY_PORT: 587
      RELAY_USERNAME: appsmith@example.com
      RELAY_PASSWORD: secretpassword
```
-  Open an ngrok terminal the following command
` ngrok tcp 25 `
- Connect a new DataSource in Appsmith from SMTP
- Host and port are given by ngrok
- The password and username are ` admin`
` note: You must have an email configured correctly to send mail `
# Connect ArangoDB container with Appsmith
- Create ArangoDB docker-compose.yml
```
version: '3.7'
services:
  arangodb_db_container:
    image: arangodb:3.2.2
    environment:
      ARANGO_ROOT_PASSWORD: rootpassword
    ports:
      - 8529:8529
```
- Open an ngrok terminal the following command
 `ngrok tcp 8529`
- Connect a new DataSource in Appsmith from ArangoDB
- Host and port given by ngrok 
- Database name:` _system`
- User: `root`
- Password: `rootpassword `