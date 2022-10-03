# DOCKER commands

--------

![](https://miro.medium.com/max/677/0*yw6M6IMB3wa02l9u)



https://medium.com/zenofai/how-to-build-a-node-js-and-mongodb-application-with-docker-containers-15e535baabf5



##### Play with Docker

https://training.play-with-docker.com/ops-s1-images/



##### Download and install

`curl -sSL https://get.docker.com | sh`

oppure

```
sudo apt install docker.io
```



##### Add current user to docker group

```
sudo usermod -aG docker $USER
```



##### Add 'pi' user to docker users

`sudo usermod -aG docker pi`

Please note: logoff and logon to complete run command or reboot.

`sudo reboot`



##### Verify Docker 

`docker --version`

`docker run armhf/hello-world`



##### List running containers

`docker container ls`

or

`docker ps`



##### List entire command

`docker ps -a --no-trunc`



##### Find all Docker images on your system

`docker images`



##### Remove an image from docker

`docker rmi nodered/node-red-docker --force`



##### Download Nodejs image

`docker pull arm32v7/node`



##### Show port in use

`sudo netstat -pant | grep 8086`



##### List states of docker containers

`docker ps -a`



##### List docker machines

`docker-machine ls`



##### List all containers

`docker ps -all`



##### Clear ALL logs (all containers)

`sudo su`
`ls /var/lib/docker/containers/*/*-json.log`
`truncate -s 0 /var/lib/docker/containers/*/*-json.log`



##### Docker login

```
docker login

username : clabnet
```



##### Run a shell command inside a particular container

`docker exec -it <container name> /bin/bash`

to get a **bash** shell **in the container**.

OR 

```
docker run -it --rm -v s:/data datalust/seq shell
```



##### Clone container (snapshot)

https://gist.github.com/thaJeztah/8d0e901bd21329d80cf2

```
docker commit --message="Ubuntu 18.04 with docker" hassio ubuntu_with_docker:20190524
```



##### Quit from docker container

`Ctrl+p`, `Ctrl+q` will now turn interactive mode into daemon mode



##### Install Portainer

https://portainer.readthedocs.io/en/latest/deployment.html



Install and start Portainer **(on Linux)**

```
docker run -d -p 9000:9000 --name portainer --restart always -v /var/run/docker.sock:/var/run/docker.sock -v /share/appdata/portainer:/data portainer/portainer
```



##### Run Portainer **(on Windows)**

```
docker run -d -p 9000:9000 -v \\.\pipe\docker_engine:\\.\pipe\docker_engine portainer/portainer:latest
```



##### How much space these log files actually take on your system

```
journalctl --disk-usage
```



##### Remove all unused images 

https://linuxize.com/post/how-to-remove-docker-images-containers-volumes-and-networks/#remove-dangling-images

```
docker image prune -a
```



##### Remove all containers stopped

```
docker container prune --filter "until=24h"
```



##### Remove container

```
docker rm <container name>
```



##### Remove all containers ( WARNING ! )

```
docker rm $(docker ps -aq) -f
```



--------

https://devhints.io/docker

https://hackernoon.com/docker-commands-the-ultimate-cheat-sheet-994ac78e2888

https://www.raspberrypi.org/blog/docker-comes-to-raspberry-pi/

http://www.ethernetresearch.com/geekzone/docker-container-tutorial-installing-docker/





- Add the docker group if it doesn't already exist:

  ```
  sudo groupadd docker
  ```

- Add the connected user "$USER" to the docker group. Change the  user name to match your preferred user if you do not want to use your  current user:

  ```
  sudo gpasswd -a $USER docker
  ```

- Either do a `newgrp docker` or log out/in to activate the changes to groups.

- You can use 

  ```
  docker run hello-world
  ```

  to check if you can run docker without sudo.



##### Create image from dockerfile

The process to run Dockerfile is:

```
docker build . -t [tag] -f /path/to/Dockerfile
```

And then:

```
docker run -d tag
```



##### Docker Inspect

```
docker inspect --format="{{json .Mounts}}" 1ef4ff22a7af
```

`[{"Type":"bind","Source":"/usr/share/hassio","Destination":"/data","Mode":"","RW":true,"Propagation":"rprivate"},{"Type":"bind","Source":"/var/run/dbus","Destination":"/var/run/dbus","Mode":"","RW":true,"Propagation":"rprivate"},{"Type":"bind","Source":"/var/run/docker.sock","Destination":"/var/run/docker.sock","Mode":"","RW":true,"Propagation":"rprivate"}]`
`root@hassios3:/home/clab#`



##### Get command line of container

```
docker inspect -f '{{ .Config.Env}} {{ .Config.Entrypoint}} {{ .Config.Cmd}} {{ .Mounts}}' 1ef4ff22a7af
```



##### Copy volumes of container

```
docker run --rm --volumes-from=5d99750f0ce3 debian tar cvf - /usr/share/hassio/homeassistant | gzip > hassios3-config.tar.gz
```

```
docker run --rm --volumes-from 5d99750f0ce3 -v ~/backup:/backup ubuntu bash -c “cd /usr/share/hassio/homeassistant && tar cvf /backup/hassios3-config.tar .”
```





https://joshuachini.com/2017/08/21/lessons-learned-while-working-with-databases-in-docker/





### docker-compose

##### start 

```
docker-compose up -d
```





### Troubleshooting

##### Issue #1

`docker: Error response from daemon: cgroups: cannot find cgroup mount destination: unknown.`

```
sudo mkdir /sys/fs/cgroup/systemd
sudo mount -t cgroup -o none,name=systemd cgroup /sys/fs/cgroup/systemd
```



##### Issue #2

`Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?`

```
Avviare docker desktop
```



##### Issue #3

`Error with docker-compose: docker-credential-desktop not installed or not available in PATH`

```
I had the same issue and noticed that there was a typo in the ~/.docker/config.json :
(Togliere la "s" da credsStore)
{
  "credStore": "desktop.exe"
}
```

