# centos7-systemd
Imagem Docker do Centos 7 com Systemd


# Docker Centos 7 with Systemd

## Introdução:

Estou criando esta imagem para futuros projetos e instalações onde usarei esta imagem que é a base para do Centos 7 com o Systemd.

Usei como referência o site oficial do Container Centos: [Oficial Repository Centos](https://hub.docker.com/_/centos/)

##Dockerfile:

A seguir mostro o arquivo Dockerfile criado para gerar a imagem ```renizgo/centos7-systemd```:

```
FROM centos:7

LABEL Renato Diniz <renatocabelo@gmail.com>

ENV container docker

RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == \
systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;

VOLUME [ "/sys/fs/cgroup" ]

CMD ["/usr/sbin/init"]
```

## Comando para gerar a Imagem Docker

Dentro do diretório onde existe o Dockerfile:

```
docker build --rm -t renizgo/centos7-systemd .
```

No caso de sucesso na geração da imagem aparecerá uma mensagem semelhante:

```
$ docker build --rm -t renizgo/centos7-systemd .
```

```
Sending build context to Docker daemon   2.56kB
Step 1/6 : FROM centos:7
 ---> 328edcd84f1b
Step 2/6 : LABEL Renato Diniz <renatocabelo@gmail.com>
 ---> Running in 2fec7f39d8b7
 ---> e637b7473178
Removing intermediate container 2fec7f39d8b7
Step 3/6 : ENV container docker
 ---> Running in dadef7cfcbb2
 ---> a389d02b908c
Removing intermediate container dadef7cfcbb2
Step 4/6 : RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); rm -f /lib/systemd/system/multi-user.target.wants/*;rm -f /etc/systemd/system/*.wants/*;rm -f /lib/systemd/system/local-fs.target.wants/*; rm -f /lib/systemd/system/sockets.target.wants/*udev*; rm -f /lib/systemd/system/sockets.target.wants/*initctl*; rm -f /lib/systemd/system/basic.target.wants/*;rm -f /lib/systemd/system/anaconda.target.wants/*;
 ---> Running in 4faec48a5556
 ---> d80e070ac465
Removing intermediate container 4faec48a5556
Step 5/6 : VOLUME /sys/fs/cgroup
 ---> Running in 2fc785758ac3
 ---> 1a2caf75ec26
Removing intermediate container 2fc785758ac3
Step 6/6 : CMD /usr/sbin/init
 ---> Running in 1d8a611f08c2
 ---> 6d01b2d1d581
Removing intermediate container 1d8a611f08c2
Successfully built 6d01b2d1d581
Successfully tagged renizgo/centos7-systemd:latest
```

# Publicando a imagem

Com o comando ```docker images``` você consegue visualizar a imagem criada:

```

Renato-Mac:renizgo_centos7-systemd renato$ docker images
REPOSITORY                TAG                 IMAGE ID            CREATED             SIZE
renizgo/centos7-systemd   latest              6d01b2d1d581        2 minutes ago       193MB
```

Faça o login no Hub Docker:

```
$ docker login
```

```
Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username (renizgo): renizgo
Password:
Login Succeeded
```

Publique a imagem com o seguinte comando:


```
$ docker push renizgo/centos7-systemd
```
```
The push refers to a repository [docker.io/renizgo/centos7-systemd]
acf87db3d826: Pushed
b362758f4793: Mounted from library/centos
latest: digest: sha256:73bf8db1007c11b7957d69de27f9431a2d79c802a0dd50075b6a1e57a3f4fbe8 size: 737
```

## Imagem Publicada: 

![alt text](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "renizgo/centos7-systemd")



