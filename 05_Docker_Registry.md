## Docker Registry

* When we run `docker run  nginx`, it actually means `docker run docker.io/nginx/nginx`
```console
$ docker run [Registry]/[User account]/[Image repository]
$ docker run nginx
$ docker run docker.io/nginx/nginx
```

## Using image from private registry

1. Login to private registry before pulling or pushing
```console
$ docker login private-registry.io
```

2. Run image from private registry 
```console
$ docker run private-registry.io/apps/internal-app
```

## Deploy Private Registry in your device using docker image "registry"

1. Run registry container (Using port 5000 by default)
```console
$ docker run -d -p 5000:5000 --name registry registry:2
```

2. Tag the image with registry's url before pushing
```console
$ docker image tag my-image localhost:5000/my-image
```

3. Push your image to registry
```console
$ docker push localhost:5000/my-image
```

4. Pull image from private registry
```console
$ docker pull localhost:5000/my-image
$ docker pull 192.168.56.100:5000/my-image
```








