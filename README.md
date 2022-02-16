# docker_learning
<h1 align="center">Learn Docker Zero to Hero</h1>


## Preface
### docker installation in ubuntu
``` sudo apt install docker.io -y ```

### start docker daemon
``` sudo systemctl start docker ```


### enable docker on startup
``` sudo systemctl enable docker ```

### verify the docker version
``` docker --version ```

<p>There is a good chance that if you are not performing commands as the root user, ypu will be not be able to run <br> majority of the commands needed. if you run the example following command, you may experience an access issue connectig <br> to the <strong>Docker</strong> daemon <br></p>

``` docker ps ```

```
Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/json: dial unix /var/run/docker.sock: connect: permission denied
```
<p>To resolve this, add current user to the <strong>Docker</strong> group<br></p>

``` sudo usermod -aG docker ${USER} ```

<p>To activate these changes, restart computer or create new session for your current user <br></p>

``` sudo su ${User} ```
<p> Run the <strong>Docker ps</strong> command again to ensure that user changes were successfull <br> </p>

``` docker ps ```

## useful <strong>Docker</strong> commands
### docker pull
``` docker pull <image_name> ```

### docker build
``` docker build -t <image_name> . ``` 

### docker run 
``` docker run --name <container_name> -d -p <localPort>:<containerPort> <image_name> ```
<p>-d - detach </p>
<p>-p - publish </p>

### stop running container
``` docker stop <container_name> ``` <br>
``` docker stop <container_id> ``` <br>
``` docker kill <container_id> ``` <br>
``` docker kill <container_name> ``` <br>

### start docker container
``` docker start <container_name> ``` <br>
``` docker start <container_id> ``` <br>

### restart docker container
``` docker restart <container_name> ``` <br>
``` docker restart <container_id> ``` <br>

### list all docker images
``` docker images ``` <br>

### list all running containers
``` docker ps ``` <br>
``` docker container ls ``` <br>

### list all container (with stopped)
``` docker ps -a ``` <br>
``` docker container ls --all ``` <br>

### docker retag (add new name)
``` docker tag <currentName>:<newName> ```

### delete stopped docker container
``` docker rm <container_name> ``` <br>
``` docker rm <container_id> ``` <br>
``` docker container rm <container_id> ``` <br>
``` docker container rm <container_name> ``` <br>
    <p> delete multiple containers <br> </p>
``` docker container rm <container_name1> <container_name2> ``` <br>

### delete docker image
``` sudo docker rmi <image_name> ``` <br>
``` sudo docker rmi <image_container> ``` <br>
``` sudo docker image rm <image_name> ``` <br>
    <p> force delete - even if image <strong>IN_USE</strong> by a container <br> </p>
``` sudo docker image rm <image_name> -f ``` <br>

### delete all containers & images & volumes
``` docker system prune -a ```


## Dockerfile
### What is Dockerfile
<p> A <strong>Dockerfile</strong> is the text file that contains instructions on how to create a Docker image <br>

<p> The format of a <strong>Dockerfile</strong> is as follows: <br> </p>

```
# This is a comment 
DIRECTIVE argument
```
<ul>
    <li> currently <strong>Dockerfile</strong> supports single line comments only </li>
    <li> <strong> Dockerfile </strong>are not case-sensitive. Even though the <strong> DIRECTIVE </strong>  is case-insensitive, it is a best practice to write all directives in uppercase to distinguish them from arguments</li>
</ul>
 

## Common DIRECTIVES in Dockerfile
<ol>
    <li> <strong> FROM </strong></li>
    <li> <strong> LABEL </strong></li>
    <li> <strong> RUN </strong></li>
    <li> <strong> CMD </strong></li>
    <li> <strong> ENTRYPOINT </strong></li>
</ol>

### The <strong> FROM </strong> Directive
<p> A <strong>Dockerfile </strong> usually starts with the <strong>FROM</strong> directive. This used to specify parent image of our customer Docker image. Ubuntu, CentOS, Nginx and MySQL are some of examples for parent images. The <strong>FROM</strong> directive takes valid image name and a tag as arguments. If the tag is not specified, the latest tag will be used <br> </p>

```
FROM <image>:<tag>

FROM scratch
```

### The <strong> LABEL </strong> Directive
<p> A LABEL is a key-value pair that can be used to add metadata to a Docker image. These labels can be used to organize the Docker images properly <br> </p>

```
LABEL <key>=<value>

LABEL maintainer=shenal@mydomain.com
LABEL version=1.0
LABEL environment=dev
```

<p> to see existing <strong>LABEL</strong> </p>

``` docker image inspect <image_name> ```


### The <strong> RUN </strong> Directive
<p> The <strong>RUN</strong> directive is used to execute commands during the image build time. This will create a new layer on top of the layer existing. The <strong>RUN</strong> directive used to install and update required packages </p>

``` RUN <command> ```

```
RUN npm install
RUN apt-get update
RUN apt-get install nginx-y

RUN npm install && npm test
```

### The <strong> CMD </strong> Directive
<p> A Docker container is normally expected to run one process. A <strong>CMD</strong> directive as used to provide this default initialization command that will be executed when a container is created from Docker image. A <strong>Dockerfile</strong> can executes only one CMD directive. If there is more than one CMD directive in the <strong>Dockerfile</strong>, Docker will execute only the last one.</p>

```
CMD ["executable", "param1", "param2", "param3", ...]

CMD ["echo", "Hello World"]
```

<p> However, if we send any command-line arguments with <strong> docker container run image, </strong>these arguments will replace over the <strong>CMD</strong> command that we defined</p>

<p> Both <strong>RUN</strong> and <strong>CMD</strong> directives used to execute a shell command. The main difference between these two directives is that the command provided with <strong>RUN</strong> directive will be executed during the image build process, while the command provided with the <strong>CMD</strong> directive will be executed once a container is launched from the build image </p>


### The <strong> ENTRYPOINT </strong> Directive
<p>Similar to the <strong>CMD</strong> directive, the <strong>ENTRYPOINT</strong> directive is also used to provide this default initialization command that will be executed when a container is created from the Docker image. The difference between the <strong>CMD</strong> directive and the <strong>ENTRYPOINT</strong> directive is that, unlike <strong>CMD</strong> directive, we cannot override the ENTRYPOINT command using the command-line parameters sent with docker container run command</p>

NOTE:
<p><strong>--entrypoint</strong> flag can be sent with the <strong>docker container run</strong> command to override the default <strong>ENTRYPOINT</strong> of the image</p>

<p>We can use <strong>CMD</strong> directive with the <strong>ENTRYPOINT</strong> directive to provide additional arguments to the executable</p>

```
ENTRYPOINT ["echo", "Hello"]
CMD ["World"]
```


### Other <strong> Dockerfile </strong> Directives
<p> Some other useful directives</p>
<ol>
    <li> <strong>ENV</strong> Directive</li>
    <li> <strong>ARG</strong> Directive</li>
    <li> <strong>WORKDIR</strong> Directive</li>
    <li> <strong>COPY</strong> Directive</li>
    <li> <strong>ADD</strong> Directive</li>
    <li> <strong>USER</strong> Directive</li>
    <li> <strong>VOLUME</strong> Directive</li>
    <li> <strong>EXPOSE</strong> Directive</li>
    <li> <strong>HEALTHCHECK</strong> Directive</li>
    <li> <strong>ONBUILD</strong> Directive</li>
</ol>

<h3> The ENV Directive </h3>
<p> The <strong>ENV</strong> directive is used to set the environment variables</p>

```
ENV <key> <value>

ENV PATH $PATH:/usr/local/bin

# set multiple env variables
ENV PATH=$PATH:?usr/local/bin VERSION=1.0.0
```

<h3> The ARG Directive </h3>
<p> the ARG directive is used to define variables that the user can pass at build time.</p>

```
docker build -t <image>:<tag> --build-arg <varName>=<value> .
```
in Dockerfile
``` 
ARG <varname>

ARG USER
ARG VERSION
```
<p> ARG directive can also have an optional default value defined. Unlike ENV variables, ARG variables are not accesble from the running container </p>

<br>
<h3>The WORKDIR Directive </h3>
<p> the WORKDIR directive is used to specify the current working directory of the Docker container. Any subsequent <strong>ADD CMD COPY ENTRYPOINT</strong> and <strong>RUN </strong>directives will be executed in this directory. </p>

```
WORKDIR /path/to/workdir
```
<br>

<h3>The COPY Directive</h3>
<p>The <strong>COPY</strong> directive can be used to copy files and folders from the local filesystem to the Docker image during the build process.</p>

```
COPY <source> <destination>

COPY . .
```
<br>

<h3>The ADD Directive</h3>
<p> The <strong>ADD</strong> directive is also similar to the <strong>COPY</strong> but however in addition it allows us to use URL as the <strong>source</strong> parameter</p>

```
ADD <source> <destination>

ADD http://localhost:3000/sample.txt /dir
```

<br>

<h3>The USER Directive</h3>
<p>Docker will use the root user as the default user of a Docker container. We can use the USER directive to change this default behavior and specify a non-root user as the default user of a Docker container</p>

```
USER <user>

USER coderx
```

<br>
