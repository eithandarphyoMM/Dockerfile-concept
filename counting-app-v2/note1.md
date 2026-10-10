build: ## Build docker image
	docker build -t $(IMAGE_NAME):$(VERSION) .

    #docker build -t counting-app:0.1 .

<!-- START: Verify Local Docker Images -->
### Verify Local Image List

Run the following command to check your built images:

```bash
$ docker images
IMAGE              ID             DISK USAGE   CONTENT SIZE   EXTRA
counting-app:0.1   710ee0b14282       16.4MB         5.36MB

```bash
$docker image inspect counting-app:0.1
[
    {
        "Id": "sha256:710ee0b14282a39c89279801203fbc9afb325b230ba1eeb7c24ae7f0dc0f6532",
        "RepoTags": [
            "counting-app:0.1"
        ],
        "Created": "2026-10-10T05:53:41.295918428Z",
        "Config": {
            "ExposedPorts": {
                "9002/tcp": {}
            },
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "PORT=9002"
            ],
        },
        "Architecture": "arm64",
        "Os": "linux",
        "Size": 16350646,
        "Metadata": {
            "LastTagTime": "2026-10-10T05:53:41.442002345Z"
        },
    }
]

run: ## run docker image locally
	docker run -it $(IMAGE_NAME):$(VERSION)

    #docker run -it counting-app:0.1

<!-- START: Interactive Container and ADD Instruction Verification -->
### Verifying File Copying with `ADD . /app`

Run the container in interactive mode to confirm that files were successfully copied into the working directory:

```bash
$ docker run -it counting-app:0.1
/app # cd ..
/ # cd /app/
/app # ls -la
total 6272
drwxr-xr-x    1 root     root          4096 Oct 10 05:53 .
drwxr-xr-x    1 root     root          4096 Oct 10 06:05 ..
-rw-r--r--    1 root     root           227 Oct 10 05:40 Dockerfile
-rw-r--r--    1 root     root           113 Oct 10 05:53 README.md
-rwxr-xr-x    1 root     root       6404610 Feb 17  2022 counting-service
/app # exit