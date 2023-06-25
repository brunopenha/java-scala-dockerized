## Compose sample application

### Use with Docker Development Environments

You can open this sample in the Dev Environments feature of Docker Desktop version 4.12 or later.

### Spark Java

Project structure:
```
.
├── compose.yaml
├── Dockerfile
├── README.md
└── src
    └── ...
```

[_compose.yaml_](compose.yaml)
```
services:
  java-scala-dockerized:
    build: .
    ports:
    - 8080:8080
```
The compose file defines an application with one service `java-scala-dockerized`.
When deploying the application, docker compose maps port 8080 of the java-scala-dockerized service container to port 8080 of the host as specified in the file.
Make sure port 8080 on the host is not already being in use.

## Deploy with docker compose

```
$ docker compose up -d
[+] Building 2.2s (16/16) FINISHED                                                                                                                               
 => [java-scala-dockerized internal] load build definition from Dockerfile                                                                                  0.0s
 => => transferring dockerfile: 781B                                                                                                                        0.0s
 => [java-scala-dockerized internal] load .dockerignore                                                                                                     0.1s
...
[+] Running 2/2
 ✔ Network java-scala-dockerized_default                    Created                                                                                         0.1s 
 ✔ Container java-scala-dockerized-java-scala-dockerized-1  Started                                                                                         0.6s ```

## Expected result

Listing containers must show one container running and the port mapping as below:

```bash
$ docker ps
CONTAINER ID   IMAGE                           COMMAND                  CREATED          STATUS          PORTS                                       NAMES
229465b887af   java-scala-dockerized-project   "/bin/sh -c 'java -j…"   11 minutes ago   Up 11 minutes   0.0.0.0:8080->8080/tcp, :::8080->8080/tcp   java-scala-dockerized-project-1
```

After the application starts, navigate to `http://localhost:8080` in your web browser or run:
```
$ curl localhost:8080
Hello from Docker!
```

Stop and remove the containers
```
$ docker compose down
[+] Running 2/2
 ✔ Container java-scala-dockerized-project-1  Removed                                                                                                      10.5s 
 ✔ Network java-scala-dockerized_default      Removed 
 ```
