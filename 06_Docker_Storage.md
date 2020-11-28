## Docker Storage

* __Docker file system :__ If your're looking for docker related files, checkout `/var/lib/docker`
```
/var/lib/docker    
│
└───aufs/            #> Storage driver for Debian
│
└───containers/      #> Checkout online docs for more info
│
└───image/
│
└───volumes/         #> Volumes that created by `docker volume create [name of volume]`
```
* __Note :__
1. Image consists of multiple layers.
2. Once the images are built, they will not be rebuilt unless you change the Dockerfile.
3. If there's only one changes in Dockerfile, only one new layer will be rebuilt.
4. All the modifications in the container will not be saved to image since image layer are "Read only" layers.
5. Use volumes to save all the changes in the container.

* Create a volume before mounting it to container
```console
$ docker volume create data_volume
#> A new volume folder will be created under /var/lib/docker/volumes
```

* Mount an existing volume to container
```console 
$ docker run –v data_volume:/var/lib/mysql mysql
$ docker run –v data_volume2:/var/lib/mysql mysql
#> New folder will be create under /var/lib/docker/volumes automatically
```

* Find out what storage driver that docker is using, run
```console
$ docker info
#> See Storage driver : aufs (Storage driver for debian)
```

* Checkout image building history
```console
$ docker history [image ID or image name]
```

* The size of the docker image you see from `docker images` is not the actual disk consumption, since images are form by multiple layers
different images and they might share the same layers. To figure out the disk consumption by docker, run
```console
docker system df
docker system df -v 
#> see SHARED_SIZE, (means they're using same layers)
```







