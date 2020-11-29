## Default Network in Docker

<div align=center>

![image](https://github.com/alonzo3569/Docker_tutorial/blob/main/Img/Docker_Default_Network.JPG)


</div>

* __Bridge :__ local area network in docker host, each container can communicate with other using internal IP. Map the port to access container from the outsidde world(ex. Browser outside VM).
* __None :__ Container is not attach to any network. Can't access from any network. It's isolated.
* __Host :__ Container can be accessed without port mapping. However, the host port will be occupied.

## Network Command

* __Identify the number of networks that exist on this system :__
```console
$ docker network ls
```
* __Select a network type for container :__
```console
$ docker run --name alpine-2 --network=none alpine
#> --network : none, host, bridge
```

* __Network information :__
```console
$ docker inspect [network ID or name]
```

* __Create a new network :__
```console
$ docker network create --driver bridge --subnet 182.18.0.1/24 --gateway 182.18.0.1 wp-mysql-network
```

* __Attach container to existing network :__
```console
$ docker run --name mysql-db -e MYSQL_ROOT_PASSWORD=db_pass123 --network wp-mysql-network mysql:5.6
```

Deploy a web application named webapp, using image kodekloud/simple-webapp-mysql. 
Expose port to 38080 on the host. 
The application takes an environment variable DB_Host that has the hostname of the mysql database. 
Make sure to attach it to the newly created network wp-mysql-network.

docker run --network=wp-mysql-network -e DB_Host=mysql-db -e DB_Password=db_pass123 -p 38080:8080 --name webapp --link mysql-db:mysql-db -d kodekloud/simple-webapp-mysql

Q: link?
