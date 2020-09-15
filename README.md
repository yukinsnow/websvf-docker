**This instruction is a guide for making the docker image for Websvf. ** 

The image is base on ubuntu official image on docker hub.  

1.Get the Ubuntu image from docker hub  

```shell
$ docker push ubuntu
```

2.Generate a container using ubuntu's image

```shell
$ docker run -itd --name ubuntu ubuntu
```

3.Enter the bash in the container

```shell
$ docker exec -it ubuntu /bin/bash
```

4.Update ubuntu

```shell
$ apt update
$ apt upgrade
```

5.Install environment

```shell
$ apt install sudo curl nodejs npm yarn
```

6.Install code-server

```shell
$ curl -fsSL https://code-server.dev/install.sh | sh
```

7.Run it first, it will generate a config file.

```shell
$ code-server
```

8.Modified config file to disable password. If you need, install nano or vim to edit text. I use nano and set "auth = none"

```shell
$ nano ~/.config/code-server/config.yaml
```

9.Commit an image. "ubuntu" is the container name you used, you can use its hash tag too

```shell
$ docker commit ubuntu coder
```

10.Run a new container using the image you created. Ths first "coder" is the container name, second is the image name. You can use the tag also 

```shell
$ docker run -d -p 8080:8080 --name coder coder code-server /home --host 0.0.0.0 --port 8080
```

11.Open you browser and test it

`` http://localhost:8080/ ``



**To be continued.**

To install the websvf, you need to copy the vsix to the container and install its environment. These steps will before step 9. After all setup up, pack the container.
