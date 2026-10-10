https://github.com/hashicorp/demo-consul-101/blob/main/k8s/dashboard-service/Makefile

build: ## Build docker image
	docker build -t $(IMAGE_NAME):$(VERSION) .
    docker build -t dashboard-app:1.0 .

```bash
docker build -t dashboard-app:1.0 .
[+] Building 1.6s (9/9) FINISHED                                                                                                                                                             docker:desktop-linux
 => [internal] load build definition from Dockerfile                                                                                                                                                         0.0s
 => => transferring dockerfile: 265B                                                                                                                               
 => => transferring context: 2B                                                                                                                                                                              0.0s
 => [1/3] FROM docker.io/library/alpine:3.24.2@sha256:294b683cb724975bec92580e1e685676bd4b50bda910ddb8c51d4cabeaec77e6                                                                                       0.0s
 => [internal] load build context                                                                                                                                                                            0.1s
 => => transferring context: 8.00MB                                                                                                                                                                          0.1s
 => CACHED [2/3] WORKDIR /app                                                                                                                                                                                0.0s
 => [3/3] ADD . /app                                                                                                                                                                                         0.0s
 => exporting to image                                                                                                                                                                                                                                              

#create repository on Docker Hub
Pushing images
You can push a new image to this repository using the CLI:

docker tag local-image:tagname new-repo:tagname

Docker commands
To push a new tag to this repository:

docker push eithandarphyo0011/dashboard-app:tagname

docker tag $(IMAGE_NAME):$(VERSION) $(IMAGE_NAME):$(VERSION)
docker tag dashboard-app:1.0 eithandarphyo0011/dashboard-app:1.0

docker images
                                                                                                                                                                                              i Info →   U  In Use
IMAGE                                 ID             DISK USAGE   CONTENT SIZE   EXTRA
dashboard-app:1.0                     6130f5ee8ab6       25.7MB         8.36MB        
eithandarphyo0011/dashboard-app:1.0   6130f5ee8ab6       25.7MB         8.36MB        

docker push new-repo:tagname
Make sure to replace tagname with your desired image repository tag.

push: ## docker push the service images
	docker push $(IMAGE_NAME):$(VERSION)
    docker push eithandarphyo0011/dashboard-app:1.0

https://hub.docker.com/repository/docker/eithandarphyo0011/dashboard-app/tags

run: ## run docker image locally
	docker run -it $(IMAGE_NAME):$(VERSION)

    Execute the container with port mapping and detached mode:
    docker run -d -p 9002:9002 --name dashboard-app counting-app:3.0