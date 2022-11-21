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
#> -f : if there're many dockerfile in the same folder, use -f to specify which dockerfile should be built
#> In this case, docker will build a image named my-simple-webapp and tag:lastest (my-simple-webapp:lastest)
$ docker build . -t [account name]/[application name]
#> use this if you want to push to dockerhub later
```

**Note :** Meaning of "." in docker build <br>
"." 不代表build該目錄底下的Dockerfile, 而是代表將目前路徑下的所有資料夾帶到docker build的環境中, 所以若和Dockerfile位置不同, 請加入-f宣告Dockerfile位置

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
```console
EXPOSE 8080
WORKDIR /opt
ENTRYPOINT ["python", "app.py"]

CMD command param1
CMD ["command","param1"] #> json format
CMD sleep 5
CMD ["sleep","5"]
```

What if you want to change the second it sleeps?  
Overwrite by docker run command  
$ docker run ubuntu-sleeper sleep 10  

It will be better if we can just input 10.  
For example : `$ docker run ubuntu-sleeper 10`  
Solution : Entrypoint  
```console
ENTRYPOINT["sleep"]  

$ docker run ubuntu-sleeper 10  
```
In case of the CMD, the cmd and params passed in will get replace.  
Whereas in case of ENTRYPOINT, the cmd params will get appended.  

While using ENTRYPOINT, if we don't specify seconds for sleep command,it will cause error.  
```console
$ docker run ubuntu-sleeper  
#> sleep: missing operand  
#> we hope it can has an initial value while no value is entered  
```
To solve this, use both CMD and ENTRYPOINT combine  
```console
ENTRYPOINT["sleep"]
CMD ["5"]
#> sleep 5
#> CMD will be appended after ENTRYPOINT
$ docker run --entrypoint sleep2.0 ubuntu-sleeper 10
```



## Save current container as image
* Run `docker commit`
```console
$ docker commit [container ID] [image tag]
$ docker commit -m "gazebo + urdf_tutorial" -a "logan" 975e48dbcc98 urdf_tutorial
#> -m : commit message
#> -a : author
```

## Checkout image commit history
* Run `docker history`
```console
$ docker history [image name or ID]
$ docker history urdf_tutorial
```
## Push local image to dockerhub
1. Login to your account
2. Tag your image with your dockerhub account before pushing it 
```console
$ docker login
$ docker tag robotx-ipc alonzo3569/robotx-ipc
$ docker push alonzo3569/robotx-ipc
```
