build: ## Build docker image
	docker build -t $(IMAGE_NAME):$(VERSION) .

    #docker build -t counting-app:3.0 .

```bash
$ docker build -t counting-app:3.0 .
[+] Building 1.6s (9/9) FINISHED                                                                                                                                                             docker:desktop-linux
 => [internal] load build definition from Dockerfile                                                                                                                                                         0.0s
 => => transferring dockerfile: 203B                                                                                                                                                                         0.0s
 => => transferring context: 2B                                                                                                                                                                              0.0s
 => [1/3] FROM docker.io/library/alpine:3.24.2@sha256:294b683cb724975bec92580e1e685676bd4b50bda910ddb8c51d4cabeaec77e6                                                                                       0.0s
 => CACHED [2/3] WORKDIR /app                                                                                                                                                                                0.0s
 => [3/3] ADD . /app                                                                                                                                                                                         0.0s
 => exporting to image                                                                                                                                                                                       0.2s
 => => exporting layers                                                                                                                                                                                      0.1s
 => => naming to docker.io/library/counting-app:3.0                                                                                                                                                          0.0s
 => => unpacking to docker.io/library/counting-app:3.0                                                                                                                                                       0.0s

<!-- START: Verify Local Docker Images -->
### Verify Local Image List

Run the following command to check your built images:

```bash
$ docker images
IMAGE              ID             DISK USAGE   CONTENT SIZE   EXTRA
counting-app:3.0   f3531ef5e4c7       23.2MB         7.51MB    U  

run: ## run docker image locally
	docker run -it $(IMAGE_NAME):$(VERSION)

    this is running on container and 
    #docker run -it counting-app:3.0

    now you need to export port to run on computer
    #docker run -d -p 9001:9001 counting-app:3.0
    http://localhost:9001/



```markdown
<!-- START: Docker Hub Tagging and Pushing Guide -->

Once your Docker image is built and verified locally, you can publish it to Docker Hub using the CLI.

#### 1. Authenticate with Docker Hub
Log into your remote registry account first:
```bash
$ docker login

```

#### 2. Tag Your Local Image

Tag your local source image with your Docker Hub username and target repository tag:

```bash
$ docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]
$ docker tag counting-app:3.0 eithandarphyo0011/counting-app:0.1

```

#### 3. Push the Image to Docker Hub

Upload your tagged image to your remote repository:

```bash
$ docker push eithandarphyo0011/counting-app:tagname
$ docker push eithandarphyo0011/counting-app:0.1

```
https://hub.docker.com/repository/docker/eithandarphyo0011/counting-app/tags
