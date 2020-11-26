## Docker Env

* Take flask app for eaxmple. if we want to chage the color of my webpage, I have to modify `app.py` in my container.
* It will be better if `app.py` is able to get the color from linux env, and then we can change linux env by using `docker run -e`.

1. Allow your python code to read linux env  
```python
os.environ.get('APP_COLOR')
#> Add this line to app.py
```

2. Run your image and input linux env
```console
$ docker run -e APP_COLOR=blue simple-webapp-color
#> -e : assign linux env
```

3. Checkout envs in your image
```console
$ docker inspect blissful_hopper
#> docker inspect [image or container ID]
#> Find "Env":[{}
```