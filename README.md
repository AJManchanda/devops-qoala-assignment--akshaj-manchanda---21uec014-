# devops-qoala-assignment--akshaj-manchanda---21uec014-

# Assignment Overview

This is a Dockerized Flask application served behind an Nginx reverse proxy. The application displays user details like IP address, MAC address, username and a timestamp.

## Files

- **Dockerfile (Python)**
- **app.py**
- **Dockerfile (Nginx)**
- **nginx.conf**
- **docker-compose.yml**

## Issues Identified and Resolution Steps

### 1. Dockerfile for Python Application

**Issues Identified:**
- The `WORKDIR` was incorrectly set as `/appp` instead of `/app`.
- The Python application file `app.py` was misnamed as `appy.py` in the `COPY` command.
- The `EXPOSE` port was set as `"eight thousand"` instead of `8000`.
- The command `CMD ["pythn", "app.py"]` contained a typo in `python`.

**Resolution:**
- Updated `WORKDIR` to `/app`.
- Corrected the filename to `app.py` in the `COPY` command.
- Updated the exposed port to `"8000"`.
- Fixed the `CMD` command to `CMD ["python", "app.py"]`.

### 2. Flask Application (app.py)

No issues were identified in the Flask application code itself. The application fetches and displays user details correctly.

### 3. Dockerfile for Nginx

**Issues Identified:**
- The base image version was specified incorrectly as `nginx:latests` instead of `nginx:latest`.
- Incorrect path and filename for the Nginx configuration file and HTML directory (`nginix.conf` and `htmll` respectively).
- Exposed port was written as `"eighty"` instead of `80`.
- The `CMD` command contained an error, using `daemon of;` instead of `daemon off;`.

**Resolution:**
- Updated the base image to `nginx:latest`.
- Corrected paths to `nginx.conf` and HTML directory.
- Set the exposed port to `80`.
- Fixed the `CMD` command to `CMD ["nginx", "-g", "daemon off;"]`.

### 4. Nginx Configuration File (nginx.conf)

**Issues Identified:**
- Configuration used `worker_process` instead of `worker_processes`.
- `worker_connection` was incorrectly specified as `worker_connection 1024;` instead of `worker_connections 1024;`.
- `mime.types` file was misnamed as `mime.typess`.

**Resolution:**
- Changed `worker_process` to `worker_processes` and `worker_connection` to `worker_connections`.
- Corrected the `mime.types` filename.

### 5. Docker Compose File (docker-compose.yml)

**Issues Identified:**
- `ports` mapping had `eighty` instead of `80:80`.
- `volumes` mapping for Nginx used `nginx.confi` instead of `nginx.conf`.
- The `python-app` service exposed `"eight thousand"` instead of `8000`.
- `networks` configuration had `bridg` instead of `bridge`.
- Missing `build` contexts for both services, resulting in Docker Compose not finding the directories for building the images.

**Resolution:**
- Updated `ports` to `80:80` and corrected `volumes` mapping to `nginx.conf`.
- Set the exposed port to `8000`.
- Corrected the network driver to `bridge`.
- Added `build` contexts for `nginx` and `python-app` services.

## Final Steps

After making these changes, the application was successfully launched using Docker Compose, accessible at `http://localhost`, and Nginx logs confirmed the requests.

## Usage

To start the application:
1. Clone the repository.
2. Navigate to the project directory.
3. Run:
   ```bash
   docker-compose up --build
