# Jenkins Configuration as Code Project

This project provides a fully automated Jenkins setup using Docker, Docker Compose, and the Jenkins Configuration as Code (CasC) plugin. The goal is to create a reproducible Jenkins environment with a pre-configured pipeline job, ready for CI/CD tasks.

The main technologies used are:
*   **Jenkins:** The core CI/CD automation server.
*   **Docker & Docker Compose:** To containerize the Jenkins server and manage its services, including a Docker-in-Docker sidecar container.
*   **Jenkins Configuration as Code (CasC):** To define the Jenkins configuration (security, jobs, etc.) in a YAML file (`casc.yaml`).
*   **Jenkins Pipeline:** A `Jenkinsfile` defines a simple pipeline that demonstrates Docker functionality within the Jenkins environment.

## Architecture

The environment is orchestrated by `docker-compose.yml`, which defines two main services:
1.  **`jenkins`:** The main Jenkins controller, built from a custom `Dockerfile`. It has the Docker CLI installed and necessary plugins. Its configuration is managed by `casc.yaml`.
2.  **`docker`:** A Docker-in-Docker (dind) service that allows the Jenkins controller to execute `docker` commands.

## Data Persistence

This project is configured to persist important data on your local filesystem, ensuring that your configurations and job history are not lost when the containers are stopped or restarted.

*   **Jenkins Home Directory:** The local `./jenkins_home` directory is mounted as a volume into the container at `/var/jenkins_home`. This includes:
    *   **Configuration as Code:** Any changes you make to `jenkins_home/casc_configs/casc.yaml` on your host machine will be automatically reloaded by Jenkins upon restart.
    *   **Job History & Workspaces:** All data related to Jenkins jobs, such as build history and workspaces, is stored here.

*   **Docker Volume:** A named volume `docker-data` is used to persist the Docker-in-Docker service's data.

---

## Getting Started

To run this project, you need **Docker** and **Docker Compose** installed on your machine.

### 1. Set the Admin Password

You can set the Jenkins admin password in one of two ways.

**Method 1: Using a `.env` file (Recommended)**

To quickly create a `.env` file with a secure password, run the following command in your terminal, replacing `your-secret-password` with a strong, unique password:

```bash
echo 'ADMIN_PASSWORD="your-secret-password"' > .env
```

This file is ignored by Git, so your password will not be committed to the repository.

**Method 2: Using an Environment Variable**

You can export the `ADMIN_PASSWORD` as an environment variable in your terminal.
```bash
export ADMIN_PASSWORD="your-secret-password"
```

**Default Password**

If the `ADMIN_PASSWORD` is not configured via a `.env` file or an environment variable *before* running `docker-compose up`, the password will default to `Admin123!`.

> **CRITICAL WARNING**
>
> It is absolutely essential to change this default password immediately after your first login for anything other than local, ephemeral testing. For any production or sensitive environment, always use a strong, unique password configured via a `.env` file or environment variable. Failure to do so poses a significant security risk.

### 2. Build and Run the Environment

Use Docker Compose to build the custom Jenkins image and start all the services in detached mode.

```bash
docker-compose up --build -d
```

### 3. Accessing Jenkins

Once the containers are running, the Jenkins UI will be accessible at `http://localhost:8080`.

You can log in with the following credentials:
*   **Username:** `admin`
*   **Password:** The password you set for the `ADMIN_PASSWORD` environment variable.

A pre-configured pipeline job named `my-public-github-repo-job` will be available on the dashboard, ready to run.

### 4. Stopping the Environment

To stop the services and remove the containers, run:

```bash
docker-compose down
```

---

## Development Conventions

### Configuration as Code

*   All Jenkins configuration should be managed through the `jenkins_home/casc_configs/casc.yaml` file. This includes security settings, credentials, and agent configurations.
*   The initial pre-configured job (`my-public-github-repo-job`) is also defined in this file. It is set up to pull the `Jenkinsfile` from this repository.

### Plugin Management

*   Jenkins plugins are managed via the `plugins.txt` file. To add, remove, or update a plugin, modify this file and rebuild the Docker image using the `--build` flag with `docker-compose up`.

### Pipeline

*   The CI/CD pipeline is defined in the `Jenkinsfile`. The sample pipeline demonstrates how to use Docker commands from within a Jenkins job. Feel free to modify it to suit your needs.