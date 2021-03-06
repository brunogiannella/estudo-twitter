# Demonstração de um serviço (SpringBoot) integrado com o API Gateway da Netflix (Zull)
O objetivo deste projeto é apresentar um case onde é consumido a API do Twitter através de um serviço feito em SpringBoot e virtualizado utilizando o Gateway de API Zuul da Netflix.

## Project

- API
	- Spring Boot

- Client
	- React

- Gateway
	- Zuul

- Discovery Service
	- Eureka (Spring Cloud)

RAML para documentar a API

## Pré-requesitos
- [Java 1.8](http://www.oracle.com/technetwork/pt/java/javase/downloads/jdk8-downloads-2133151.html)
- [Maven](https://maven.apache.org/)
- [Docker](https://docs.docker.com/engine/installation/)
- [Docker Compose](https://docs.docker.com/compose/install/)

### Construção dos Containers

***MongoDB
```bash
sudo docker run --net host -p 27000:27017 --name mongo mongo
```

***Eureka Server
```bash
cd eureka-server
mvn clean install
docker build -t eureka-server:1.0.0 .
docker run --net host -p 9671:9671 -t eureka-server:1.0.0
```

***API
```bash
cd itau-case-twitter
mvn clean install
docker build -t twitter-service:1.0.0 .
docker run --net host -p 8090:8090 -t twitter-service:1.0.0
```

***API Gateway
```bash
cd api-gateway
mvn clean install
docker build -t api-gateway:1.0.0 .
docker run --net host -p 8075:8075 -t api-gateway:1.0.0
```

***Client 
```bash
cd twitter-service-client
docker build -t twitter-service-client .
docker run --net host -p 8080:8080 -t twitter-service-client:1.0.0
```

## Execução

- Consumir os Tweets e gravar na base de dados / geração de indicadores --> POST http://localhost:8075/api/tweets/v1/tweets/processarTweets

***Payload de entrada
```bash
{
	"hashtags" : [
		"openbanking",
		"wso2",
		"raml"	
	]
}
```

- Consulta dos indicadores --> GET http://localhost:8075/api/tweets/v1/tweets?view=indicadores

## Conclusion
*******Under Construction*******

