# Docker Image

## Create your own image

1. edit Dockerfile
```console
$ vim Dockerfile
```

2. Build your image
```console
$ docker build . -t my-simple-webapp 
#> -t : assign a name for the image
#> In this case, docker will build a image named my-simple-webapp and tag:lastest (my-simple-webapp:lastest)
$ docker build . -t [account name]/[application name]
#> use this if you want to push to dockerhub later
```

3. Run your image
```console
$ docker run my-simple-webapp
```

4. Push it to dockerhub
```console
$ docker login
$ docker push [docker hub account name]/[application name]
```

* Dockerfile
```console
FROM ubuntu

RUN apt-get update
RUN apt-get install -y python python-pip
RUN pip install flask

COPY ./app.py /opt/source-code  
#> copy app.py to the container

ENTRYPOINT FLASK_APP=/opt/source-code/app.py flask run 
#> once u run your image, it will execute this command
```

EXPOSE 8080
WORKDIR /opt
ENTRYPOINT ["python", "app.py"]

CMD command param1
CMD ["command","param1"] #> json format
CMD sleep 5
CMD ["sleep","5"]

If you want to chage the second it sleep?
Overwrite by docker run command
$ docker rum ubuntu-sleeper sleep 10

It will be better if we can just input 10
For example 
$ docker rum ubuntu-sleeper 10
Solution : Entrypoint

ENTRYPOINT["sleep"]

$ docker rum ubuntu-sleeper 10

In case of the CMD, the cmd params passed will get replace
Whereas in case of ENTRYPOINT, the cmd params will get appended

While using ENTRYPOINT, if we don't specify seconds for sleep command,
it will cause error.
$ docker run ubuntu-sleeper
#> sleep: missing operand
#> we hope it can has an initial value while no value is entered

To solve this, use both CMD and ENTRYPOINT combine
ENTRYPOINT["sleep"]
CMD ["5"]
#> sleep 5
#> CMD will be appended after ENTRYPOINT

$ docker run --entrypoint sleep2.0 ubuntu-sleeper 10
