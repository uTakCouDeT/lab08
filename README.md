## Laboratory work XIII

Данная лабораторная работа посвещена изучению систем для автоматизации развёртывания и управления приложениями на примере **Docker**

```bash
$ open https://docs.docker.com/get-started/
```

## Tasks

- [ ] 1. Создать публичный репозиторий с названием **lab13** на сервисе **GitHub**
- [ ] 2. Выполнить инструкцию учебного материала
- [ ] 3. Ознакомиться со ссылками учебного материала

## Tutorial

```bash
$ export GITHUB_USERNAME=<имя_пользователя>
```

```bash
$ git clone https://github.com/${GITHUB_USERNAME}/lab12 lab13
$ cd lab13
$ git remote remove origin
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab13
```

```bash
$ cat > Dockerfile <<EOF
FROM ubuntu:16.04
EOF
```

```bash
$ cat >> Dockerfile <<EOF

RUN apt update
RUN apt install -yy gcc g++ cmake 
EOF
```

```bash
$ cat >> Dockerfile <<EOF

COPY . print/
WORKDIR print
EOF
```

```bash
$ cat >> Dockerfile <<EOF

RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install
RUN cmake --build _build
RUN cmake --build _build --target install
EOF
```

```bash
$ cat >> Dockerfile <<EOF

ENV LOG_PATH /home/logs/log.txt
EOF
```

```bash
$ cat >> Dockerfile <<EOF

VOLUME /home/logs
EOF
```

```bash
$ cat >> Dockerfile <<EOF

WORKDIR _install/bin
EOF
```

```bash
$ cat >> Dockerfile <<EOF

CMD ./demo
EOF
```

```bash
$ docker build -t logger .
```

```bash
$ docker images
```

```bash
$ mkdir logs
$ docker run -it -v "$(pwd)/logs/:/home/logs/" logger
text1
text2
text3
<C-D>
```

```bash
$ docker inspect logger
```

```bash
$ cat logs/log.txt
```

```bash
$ git add Dockerfile
$ git commit -m"adding Dockerfile"
$ git push origin master
```

## Links

- [Instructions](https://docs.docker.com/engine/reference/builder/)
- [Book](https://www.dockerbook.com)
