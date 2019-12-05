This file helps you to start with Docker and tackling with windows .Net Core applicaiton building

[Best Practices to write Docer File](https://andrewlock.net/optimising-asp-net-core-apps-in-docker-avoiding-manually-copying-csproj-files/)

Docker file is a text file having instructions understood by docker client using "docker build" command,

# Key Dockerfile instructions
* FROM
* MAINTAINER
* RUN
* COPY
* ENTRYPOINT
* WORKDIR
* EXPOSE
* ENV
* VOLUME

Typical Docker file looks like,

Command       | Value
------------  | -------------
FROM          | node
MAINTAINER    | Vinay Dev
COPY          | ./var/www 
WORKDIR       | /Var/www
RUN           | npm install
EXPOSE        | 8080
ENTRYPOINT    | ["node","server.js"]

Standar name given is "Dockerfile" by defualt, below is node.js environment
[Sample Docker File](https://forums.docker.com/t/docker-file-copy/43700)

```javascript
From node:latest      \\ always take latest version of node or you can mention version like node:5.5

MAINTAINER vinaydev   \\ who is maintaing this docker file
ENV NODE_ENV = production \\ environment settings
ENV PORT = 3000

COPY . /var/www       \\ It can copy file or entire src to \va\www directory
WORKDIR /var/www      \\sets the context for different commands to runm,from where it has to run

VOLUME ["/var/www"]   \\helps to mount this folder onto the host system

RUN npm install       \\ it runs from the work directory

EXPOSE 3000           \\any default port to expose for container

ENTRYPOINT ["npm","start"]  \\Entry point of the applicaiton

```

Docker file for .Net framework environment
* [Sample Docker File](https://hub.docker.com/r/microsoft/aspnetcore-build/),
* [How to Run Dockerfile?]( https://hub.docker.com/r/microsoft/aspnetcore),
* [Official Microsoft Docker Images](https://hub.docker.com/u/microsoft)

User docker
```javascript
From microsoft/aspnetcore-build   \\ always take latest version of aspnetcore or you can mention version like node:3.0
LABEL author = vinaydev           \\ who is maintaing this docker file
ENV ASPNETCORE_URLS=http:         \\*:5000 \\ Environment settings
ARG source =.                     \\ argument 
WORKDIR /app                      \\sets the context for different commands to runm,from where it has to run
EXPOSE 5000                       \\any default port to expose for container
COPY $source .      
ENTRYPOINT ["dotnet", "aspnetcoredocker.dll"]  \\Entry point of the applicaiton

```
# Docker Commands
* docker build -t <your username> /node . ( tag your image name)
  * $ docker build -t whenry/fedora-jboss:latest -t whenry/fedora-jboss:v2.1 . ( you can have multiple tags while building docker file)
  * $ docker tag <image> <newName>/<repoName>:<tagName> (tag build name)
  * docker build --build-arg http_proxy=http://proxy2024.scansafe.net:8080  -t aspnetapp . (if you have proxy settings in your network).
* docker build --pull -t aspnetapp . (you can pull image from dockerhub)
* docker run --name aspnetcore_sample -p 8000:80 aspnetapp
* docker run -d -p 8000:3000 aspnetapp ( d- stands for daemon mode means running background)
* docker ps -a ( show all running containers)
* docker ps ( show only running containers)
* docker rm <container id> (removes container w.r.t container ID)
* docker rmi <image_id> ( removes imaged id based on image ID)
* docker images (shows all the images)
* docker stop <container id> ( stops running container)

# VSCode Extentions:
Docker Extension : Adds syntax highlighting, commands, hover tips, and linting for Dockerfile and docker-compose files

# Sample Docker file with mulitple projects support

``` javascript
FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY Solution.sln ./
COPY ClassLibraryProject/*.csproj ./ClassLibraryProject/
COPY WebAPIProject/*.csproj ./WebAPIProject/

RUN dotnet restore
COPY . .
WORKDIR /src/ClassLibraryProject
RUN dotnet build -c Release -o /app

WORKDIR /src/WebAPIProject
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebAPIProject.dll"]

```
//If you are using private Nuget settings then <br>
https://github.com/microsoft/azure-pipelines-tasks/issues/6135 <br>
//Create Nuget.config file and add it in docker file <br>
https://github.com/dotnet/dotnet-docker/issues/463 <br>

//If you stuck in calling localhost from docker container while running then use <br>
//Run this command to test the ip address of the docker running deamon, <br>
docker network inspect bridge --format='{{( index .IPAM.Config 0).Gateway}}'

//Then based on that configure your localhost to this IP, if you have domain then you can directly call the domain. <br>
https://github.com/qoomon/docker-host

# how to modify container <br>
//Use below conatiner to get inside container and modify files inside it, below is for linux container using bash, <br>
docker exec -it "conainer ID" bash <br>
//it opens bash command prompt inside container you can view files inside it <br>

# How to edit docker image and push backto docker hub <br>
https://ropenscilabs.github.io/r-docker-tutorial/04-Dockerhub.html <br>
https://docs.docker.com/engine/reference/commandline/push/ <br>






