## Docker Compose

* Docker compose allow us to run multiple container using one command `docker-compose up`
* Docker compose does not get install by default. Follow the instructions on the official website to download docker compose.
* There're many versions of `docker-compose.yml`.

* docker-compose.yml 
```console
redis:                  #> name of the container
   image: redis         #> base image
   build: ./vote        #> build the Dockerfile in the path
   ports:
       - 5000:80        #> same as -p
   links:
       - db             #> the container you want to link
                        #> this will link redis container to db container
                        #> in redis container, use redis API to get/send data to db container
```
```console
version: '2'            #> '' is needed
                        #> can be placed at EOF
services: 
  db:
    environment:
      POSTGRES_PASSWORD: mysecretpassword
    image: postgres
  wordpress:
    image: wordpress
    links:
    - db
    ports:
    - 8085:80
    depends_on:         #> which container should be active before current container running
    - db                #> In this case, db should be running before wordpress
```



* Questions :  
docker run -d --name=wordpress --link db:db -p 8085:80 wordpress
What's 80?? => web ui using port 80 

create a simple wordpress container called wordpress, image: wordpress, 
link it to the container db and expose it on host port 8085
$ docker run -d --name=wordpress --link db:db -p 8085:80 wordpress





