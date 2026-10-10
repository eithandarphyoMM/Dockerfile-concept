# Dockerfile-concept
Step-by-Step Dockerfile Concepts by HelloCloud

# Docker Image Creation and Compose Complete Guide

This guide synthesizes notebook notes into a structured, step-by-step on Docker image creation, Dockerfile instructions, versioning workflows, Makefile automation, port mapping, and Docker Hub distribution.

---

## 📌 Core Concepts Overview

- **`docker build`**: Builds a Docker image from a `Dockerfile`. The build command must be executed within the path where the `Dockerfile` resides [1].
- **`docker-compose.yml`**: Simplifies multi-container management (e.g., `counting` service and `dashboard` service). Instead of modifying and executing individual `CMD` entries manually for each container, all service configurations are defined inside `docker-compose.yml` and started together using `docker compose up` [1].

---

## 🛠️ Step-by-Step Dockerfile & Image Creation Guide

### Phase 1: Environment Setup & Project Initialization (Steps 1–8)

1. **Clone the Source Repository**:
   Create and navigate to the project root directory (`mkdir counting-app && cd counting-app`), then clone the baseline repository using `git clone demo-console-101` [2].
2. **Remove Unused Local Configurations**:
   Delete `demo-localhost` from the project workspace [2].
3. **Organize Counting Service Binaries**:
   Move the `Dockerfile` and the `counting-service` binary file into position [2].
4. **Organize Dashboard Service Binaries**:
   Set up `dashboard-app` by moving its corresponding `Dockerfile` and `dashboard-service` binary file [2].
5. **Verify Host Architecture & OS**:
   Navigate into `counting-app` (`cd counting-app`) and check the underlying host OS to ensure the correct binary architecture was cloned [2].
6. **Clean Up Unneeded Docker Images**:
   List existing local images using `docker images` and remove outdated or unnecessary images using `docker rmi IMAGE_NAME` [2].
7. **Prepare Dockerfile for Initial Testing**:
   Open the `Dockerfile` and temporarily comment out the `ENV` and `CMD` instructions [2].
8. **Build Initial Image**:
   Execute the image build process using `docker build -t counting-app:v1 .` [2].

---

### Phase 2: Automation & Image Inspection (Steps 9–11)

9. **Create Project Documentation**:
   Create a `README.md` file in the repository root [3].
10. **Configure Build Automation with Makefile**:
    Set up a GitHub `Makefile` (Line 10: define `IMAGE_NAME:ver`). Execute the run command and monitor build step logs (e.g., `[1/3]`, `[2/3]`, `[3/3]`) to verify step execution against the `Dockerfile` [3].
11. **Inspect Built Image Metadata**:
    Run `docker image inspect img_name:ver` to examine image properties, including **Architecture**, **OS**, **Size**, **exposed ports**, and **Environment variables (`ENV`)** [3].

---

### Phase 3: Interactive Container Testing (Steps 12–14)

12. **Enter Container Environment Interactively**:
    Run the container interactively via Makefile targets (lines 16/17) using `docker run -it img-name:ver` [4]. Verify the working directory (`WORKDIR` set to `/app`) by running `cd ..`, `cd /app`, and `ls -la` [4].
13. **Understand File Copying with `ADD`**:
    Use the Dockerfile instruction `ADD . /app` to copy all local directory contents into the `/app` container path [4].
14. **Exit Container Workspace**:
    Type `exit` to terminate the interactive container session [4].

---

### Phase 4: Versioning (v2) & Dockerfile Optimization (Steps 15–18)

15. **Initialize Version 2 (`v2`) Workspace**:
    Create a new directory (`mkdir counting-app-v2`), copy all files from `v1`, rename `counting-service` to `abc-service`, and update documentation files (`note1.md`, `note2.md`, `note3.md`) [5].
16. **Update Dockerfile Instructions for v2**:
    Modify the `Dockerfile` to pull the latest base version (`FROM latest ver`), specify working directory (`WORKDIR /helloapp`), and copy files using `ADD . /helloapp` [5].
17. **Build Image v2**:
    Run `docker build -t counting-app:v2 .` to compile version 2 [5].
18. **Verify v2 Build Logs & Inspection**:
    Track execution progress across build stages (`[1/5]`, `[2/5]`) and confirm parameters using `docker image inspect` [5].

---

### Phase 5: Container Portability & Version 3 Iteration (Steps 19–22)

19. **Verify Internal Directory Layout**:
    Execute `docker run` and check container paths via CLI/GUI commands (`pwd`, `cd ..`, `ls -la`, `cd /helloapp`, `ls -la`) [6].
20. **Enable Environment & Command Instructions**:
    Uncomment (`comment in`) `ENV` and `CMD` inside the `Dockerfile`. Note that container portability allows execution across identical operating system environments [6].
21. **Iterate to Version 3 (`counting-app-v3`)**:
    Create `counting-app-v3` and test execution behavior when omitting or adjusting the `CMD` instruction [6].
22. **Clean Up Obsolete Resources**:
    Remove old images using `docker rmi <image>` and clear stopped containers using `docker rm <container>` [6].

---

### Phase 6: Port Publishing & Docker Hub Deployment (Steps 23–26)

23. **Publish Container Ports to Host**:
    Container processes run on internal ports by default [7]. Check running containers with `docker ps` and map internal ports to host computer ports using detached mode:
    ```bash
    docker run -d -p 9001:9001 img-name:ver
    ```
    *(This maps host port 9001 to container port 9001)* [7].
24. **Authenticate to Docker Hub**:
    Log into your remote registry account using:
    ```bash
    docker login
    ```
    [7].
25. **Prepare Images for Registry Push**:
    List local images with `docker images` and confirm target tags before pushing [7].
26. **Tag & Push Image to Docker Hub**:
    Use `docker tag --help` for reference. Tag your local image with your Docker Hub username and repository target:
    ```bash
    docker tag computer/source Dockerhub_username/Target_TAG
    docker push Dockerhub_username/Target_TAG
    ```
    [7].

---

## 📋 Docker CLI Command Cheat Sheet

| Command / Instruction | Description / Context | Source Ref |
| :--- | :--- | :--- |
| **`docker build`** | Builds Docker image from Dockerfile in current directory path | [1, 2, 5, 7] |
| **`docker compose up`** | Starts all services configured in `docker-compose.yml` simultaneously | [1] |
| **`docker images`** | Lists all locally stored Docker images | [2, 7] |
| **`docker rmi <IMAGE>`** | Removes specified Docker image | [2, 6] |
| **`docker rm <CONTAINER>`** | Removes stopped container instance | [6] |
| **`docker image inspect <IMG:TAG>`** | Displays architecture, OS, size, ports, and ENV variables | [3, 5] |
| **`docker run -it <IMG:TAG>`** | Runs container in interactive terminal mode | [4] |
| **`docker run -d -p 9001:9001 <IMG:TAG>`** | Runs container in detached mode with host:container port binding | [7] |
| **`docker login`** | Authenticates user session with Docker Hub | [7] |
| **`docker tag <SRC> <TARGET>`** | Tags local source image to `Dockerhub_username/Target_TAG` | [7] |
| **`docker push <TARGET>`** | Uploads tagged image to remote Docker Hub repository | [7] |