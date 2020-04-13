# Wiremock Docker Record
 
## Record mode image
 [Wiremock server](http://wiremock.org) built upon [wiremock-docker][https://github.com/rodolpheche/wiremock-docker

## Supported tags :

### Last

- TBS

### Complete list

TBS

## The image includes

- `EXPOSE 8080 8443` : the wiremock http/https server port
- `VOLUME /home/wiremock` : the wiremock data storage
- `ENV PROXY_ALL https://httpbin.org` : A simple REST service
- `ENV MATCH_HEADERS Accept,Accept-Encoding,Content-Type,Client-Token` : The headers you want to match for the mock request 

## How to use this image

#### Environment variables

- `uid` : the container executor uid, useful to avoid file creation owned by root
- `JAVA_OPTS` : for passing any custom options to Java e.g. `-Xmx128m`
- `ENV PROXY_ALL https://httpbin.org` // A simple REST service
- `ENV MATCH_HEADERS Accept,Accept-Encoding,Content-Type,Client-Token` // The headers you want to match for the mock request 

#### Getting started

##### Pull latest image

```sh
docker pull dantmcgowan/wiremock-docker-record
```

##### Build the docker container

```sh
docker build -t wiremock-docker-record .
```
##### Start the docker conainter - docker-compose

```sh
docker-compose up
```
> Access [https://localhost:8443/__admin](https://localhost:8443/__admin) to check https working

##### Stop the docker conainter - docker-compose

```sh
docker-compose down
```

> Access [http://localhost:8080/__admin](http://localhost:8080/__admin) to display the mappings (empty set)

##### Start a Wiremock container with Wiremock arguments

```sh
docker run --name wiremock-docker-record \
  -p 8080:8080 \
  -v $PWD/stubs:/home/wiremock \
  -u $(id -u):$(id -g) \
  wiremock-docker-record
```

##### Stop the docker conainter - docker-compose

```sh
docker rm -f wiremock-docker-record
```

##### After starting container, record a stub

```sh
curl --header 'Accept: application/json'\
     --header 'Accept-Encoding: deflate'\
     --header 'Content-Type: application/json'\
     --header 'Client-Token: swagger-test'\
     'http://localhost:8080/get'  
```

