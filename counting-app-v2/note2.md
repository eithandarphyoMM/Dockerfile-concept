build: ## Build docker image
	docker build -t $(IMAGE_NAME):$(VERSION) .

```bash
$ docker build -t counting-app:2.0 .
[+] Building 1.8s (11/11) FINISHED                                                                                                                                                           docker:desktop-linux
 => [internal] load build definition from Dockerfile                                                                                                                                                         0.0s
 => => transferring dockerfile: 335B                                                                                                                                                                         0.0s
 => [internal] load metadata for docker.io/library/alpine:3.24.2                                                                                                                                             1.4s
 => [auth] library/alpine:pull token for registry-1.docker.io                                                                                                                                                0.0s
 => [internal] load .dockerignore                                                                                                                                                                            0.0s
 => => transferring context: 2B                                                                                                                                                                              0.0s
 => [internal] load build context                                                                                                                                                                            0.1s
 => => transferring context: 6.41MB                                                                                                                                                                          0.0s
 => CACHED [1/5] FROM docker.io/library/alpine:3.24.2@sha256:294b683cb724975bec92580e1e685676bd4b50bda910ddb8c51d4cabeaec77e6                                                                                0.0s
 => => resolve docker.io/library/alpine:3.24.2@sha256:294b683cb724975bec92580e1e685676bd4b50bda910ddb8c51d4cabeaec77e6                                                                                       0.0s
 => [2/5] WORKDIR /hello-app                                                                                                                                                                                 0.0s
 => [3/5] WORKDIR /hellocloud-app                                                                                                                                                                            0.0s
 => [4/5] WORKDIR /counting-v2-app                                                                                                                                                                           0.0s
 => [5/5] ADD . /hellocloud-app                                                                                                                                                                              0.0s
 => exporting to image                                                                                             
 => => naming to docker.io/library/counting-app:2.0                                                                                                                                                          0.0s
 => => unpacking to docker.io/library/counting-app:2.0   

<!-- START: Verify Local Docker Images -->
### Verify Local Image List

Run the following command to check your built images:

```bash
$ docker images
IMAGE              ID             DISK USAGE   CONTENT SIZE   EXTRA
counting-app:0.1   710ee0b14282       16.4MB         5.36MB    U   
counting-app:2.0   24388d6fc726       23.3MB         7.55MB 

```bash
$docker image inspect counting-app:2.0
[
    {
        "RepoTags": [
            "counting-app:2.0"
        ],
        "Created": "2026-10-10T06:19:47.711531376Z",
        "Config": {
            "ExposedPorts": {
                "9002/tcp": {}
            },
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "PORT=9002"
            ],
            "Cmd": [
                "/bin/sh"
            ],
            "WorkingDir": "/counting-v2-app"
        },
        "Architecture": "arm64",
        "Os": "linux",
        "Size": 23317151,
        "Metadata": {
            "LastTagTime": "2026-10-10T06:19:47.867120126Z"
        },
        "Identity": {
            "Build": [
                {
                    "Ref": "ky1ubsujj8qccvp5tpkxec24g",
                    "CreatedAt": "2026-10-10T06:19:47.899495876Z"
                }
            ]
        }
    }
]

run: ## run docker image locally
	docker run -it $(IMAGE_NAME):$(VERSION)

    #docker run -it counting-app:2.0

<!-- START: Interactive Container and ADD Instruction Verification -->
### Verifying File Copying with `ADD . /hellocloud-app`

Run the container in interactive mode to confirm that files were successfully copied into the working directory:

```bash
$ docker run -it counting-app:2.0
/counting-v2-app # cd ..
/ # ls -la
total 76
drwxr-xr-x    1 root     root          4096 Oct 10 06:26 .
drwxr-xr-x    1 root     root          4096 Oct 10 06:26 ..
-rwxr-xr-x    1 root     root             0 Oct 10 06:26 .dockerenv
drwxr-xr-x    2 root     root          4096 Sep 17 17:32 bin
drwxr-xr-x    2 root     root          4096 Oct 10 06:19 counting-v2-app
drwxr-xr-x    2 root     root          4096 Oct 10 06:19 hello-app
drwxr-xr-x    1 root     root          4096 Oct 10 06:19 hellocloud-app

/ # cd hello-app/
/hello-app # ls -la
total 8
drwxr-xr-x    2 root     root          4096 Oct 10 06:19 .
drwxr-xr-x    1 root     root          4096 Oct 10 06:26 ..
/hello-app # cd ../
/ # cd counting-v2-app/
/counting-v2-app # ls -la
total 8
drwxr-xr-x    2 root     root          4096 Oct 10 06:19 .
drwxr-xr-x    1 root     root          4096 Oct 10 06:26 ..
/counting-v2-app # cd ../
/ # cd hellocloud-app/
/hellocloud-app # ls -la
total 6276
drwxr-xr-x    1 root     root          4096 Oct 10 06:19 .
drwxr-xr-x    1 root     root          4096 Oct 10 06:26 ..
-rw-r--r--    1 root     root           296 Oct 10 06:18 Dockerfile
-rwxr-xr-x    1 root     root       6404610 Oct 10 06:14 abc-service
-rw-r--r--    1 root     root          1872 Oct 10 06:14 note1.md
-rw-r--r--    1 root     root          1872 Oct 10 06:19 note2.md
