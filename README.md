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
``` docker stop <container_name> ```
``` docker stop <container_id> ```
``` docker kill <container_id> ```
``` docker kill <container_name> ```

### start docker container
``` docker start <container_name> ```
``` docker start <container_id> ```

### restart docker container
``` docker restart <container_name> ```
``` docker restart <container_id> ```

### list all docker images
``` docker images ```

### list all running containers
``` docker ps ```
``` docker container ls ```

### list all container (with stopped)
``` docker ps -a ```
``` docker container ls --all ```

### docker retag (add new name)
``` docker tag <currentName>:<newName> ```

### delete stopped docker container
``` docker rm <container_name> ```
``` docker rm <container_id> ```

### delete docker image
``` sudo docker rmi <image_name> ```
``` sudo docker rmi <image_container> ```
