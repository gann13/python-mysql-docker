# python-mysql-docker
Creating a dockerized python image with pymysql module



### myapp.py
This file contains the python source code which uses *pymysql* module and connects to mysql database to perform SQL operation

### requirements.txt
This file will contain all the required modules to be installed to support the code.


### Dockerfile
This file contains the instructions to build a customized docker image. A python base image *python:3.8-slim-buster* is used and a customized imae is built by copying source code and installing dependencies.


## Build Docker file

```sh
docker build --tag py-mysql-app .
```

```sh
Sending build context to Docker daemon  51.71kB
Step 1/6 : FROM python:3.8-slim-buster
3.8-slim-buster: Pulling from library/python
b4d181a07f80: Pull complete 
de8ecf497b75: Pull complete 
6ea9cb124572: Pull complete 
9a8aa9d08ec5: Pull complete 
360b2e4ced96: Pull complete 
Digest: sha256:bd12f13a9b40f7fbb037bb98f09bda8cbc8e214035b49913e841a5369a50fff4
Status: Downloaded newer image for python:3.8-slim-buster
 ---> 0e0d73ddd34d
Step 2/6 : WORKDIR /app
 ---> Running in bd676e5dc8ab
Removing intermediate container bd676e5dc8ab
 ---> 1b7e35afa6b8
Step 3/6 : COPY requirements.txt requirements.txt
 ---> f93f04a82d27
Step 4/6 : RUN pip3 install -r requirements.txt
 ---> Running in 97184a53833b
Collecting pymysql
  Downloading PyMySQL-1.0.2-py3-none-any.whl (43 kB)
Installing collected packages: pymysql
Successfully installed pymysql-1.0.2
WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtu
al environment instead: https://pip.pypa.io/warnings/venv
Removing intermediate container 97184a53833b
 ---> 8e8e584c6755
Step 5/6 : COPY . .
 ---> 30a513e96ed8
Step 6/6 : CMD [ "python3", "/app/myapp.py"]
 ---> Running in c6dfb0785fd6
Removing intermediate container c6dfb0785fd6
 ---> d87a2b258a74
Successfully built d87a2b258a74
Successfully tagged py-mysql-app:latest
```

## Tag docker image
```sh
docker tag py-mysql-app:latest py-mysql-app:1.0
```

## List docker image 
```sh
docker images


REPOSITORY                            TAG               IMAGE ID       CREATED         SIZE
py-mysql-app                          1.0               d87a2b258a74   2 minutes ago   120MB
```

## Run the docker image as container
```sh
docker run py-mysql-app:1.0
```




