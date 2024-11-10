# Minimal Python Docker image

(With this, I just summarized for myself: How I proceed with this short session.)

Based on the Youtube video from Christian Lempa [Docker VSCode Python Tutorial // Run your App in a Container](https://www.youtube.com/watch?v=jtBVppyfDbE&t=634s) I just did as described and build my first service from a short Python script runing in a Docker container - it is just a Hello World:

``` Python
print("Hello World! - from Docker")
```

> > docker run --rm hagen25081998/hello_from_docker
> Hello World! - from Docker

## Prerequisites

- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- [VScode](https://code.visualstudio.com/)
  - VScode Plugin for Python
  - VScode Plugin for Docker
- optional [Pipenv: Python Dev Workflow for Humans](https://pipenv.pypa.io/en/latest/) 


## Preparations
I prepare everything, as descriped by [Youtube: Docker VSCode Python Tutorial // Run your App in a Container](https://www.youtube.com/watch?v=jtBVppyfDbE&t=634s) or [Github: Docker VSCode Python Tutorial // Run your App in a Containerv](https://github.com/christianlempa/videos/tree/main/docker-python-debugging-vscode)

## Build and run the Docker image

At the prompt
``` Python
minimal_python_docker
|
|-- .dockerignore
|-- .gitignore
|-- Dockerfile        # instruction how o build the docker image
|-- hello.py          # the Python script: a one-liner
|-- Pipfile           # optional, just: python_version = "3.12"
|-- README.md         # this text you currently reading
|-- requirements.txt  # empty
```

Pipfile defined at prompt:

```shell
touch Pipfile
pipenv --python 3.12
```

Will give you:

```shell no-copy
> more Pipfile
[[source]]
url = "https://pypi.org/simple"
verify_ssl = true
name = "pypi"

[packages]

[dev-packages]

[requires]
python_version = "3.12" 
```


1. Go to the terminal at directory _minimal_python_docker_ and build a new docker image:
    ``` shell
    docker tag hello_from_docker . 
    ```
2. run the new docker image
    ``` shell
    docker run --rm hello_from_docker
    ``` 
    you will get 
    ``` shell
    > docker run --rm hello_from_docker
    Hello World! - from Docker
    ```

Docker builds images that are the templates about containers,  only that containers can be execcuted. 

If you just ```docker run <image_name>```, Docker will generate a container with a random-name in backgroud and start this container. This randomly-named container will stay and be visible in you _Docker Desktop appication_. (Do not forget to remove unsed container from your Docker Desktop from time to time.)

If you do not need that randomly-named container you can remove it.

Alternatively you can ```docker run --rm <image name>``` with the **--rm** parameter, with this docker will remove the randomly-named container after execution.

## Publish your image to Docker Hub

If you have an account at Docker Hub, you can push your image to the Docker Hub, so you can anytime run that services provided with this image from any host where a _Docker Desktop_ is installed

### 1. Login to Docker Hub

From Terminal

```shell
docker login -u ACCOUNT-NAME
````
You have to enter your password .

### 2. Build your image to push to Docker Hub

> docker tag IMAGE-NAME ACCOUNT-NAME/IMAGE-NAME

e.g.:
```shell
docker tag hello_from_docker <account name>/hello_from_docker
````

### 3. Push your image to Docker Hub

> docker push ACCOUNT-NAME/IMAGE-NAME

e.g.:
```shell
docker push <account>/hello_from_docker
````

### 4. Run your image from The Docker Hub

> docker run ACCOUNT-NAME/IMAGE-NAME

e.g.
```shell
docker run <account>/hello_from_docker
```

## Directly run my hello_from_docker image

```shell
 docker run --rm hagen25081998/hello_from_docker
 ```
you will get 
``` shell
> docker run --rm hagen25081998/hello_from_docker
Hello World! - from Docker
```
