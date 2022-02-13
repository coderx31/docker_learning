# docker_learning
learn docker zero to hero


## Preface
### docker installation in ubuntu
``` sudo apt install docker.io -y ```

### start docker daemon
``` sudo systemctl start docker ```


### enable docker on startup
``` sudo systemctl enable docker ```

### verify the docker version
``` docker --version ```

<p>There is a good chance that if you are not performing commands as the root user, ypu will be not be able to run <br> majority of the commands needed. if you run the example following command, you may experience an access issue connectig <br> to the **Docker** daemon</p>
<br>
``` docker ps ```
<br>
```
Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/json: dial unix /var/run/docker.sock: connect: permission denied
```
<br>
<p>To resolve this, add current user to the **Docker** group<br></p>
``` sudo usermod -aG docker ${USER} ```
<br>
<p>To activate these changes, restart computer or create new session for your current user <br></p>

``` sudo su ${User} ```
<br>
<p> Run the **Docker ps ** command again to ensure that user changes were successfull <br> </p>
``` docker ps ```
<br>
