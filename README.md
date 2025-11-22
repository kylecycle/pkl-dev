# PKL Docker Dev Environment

This repository provides a simple and reproducible Docker-based environment for evaluating Apple PKL files and outputting JSON. It supports two workflows:

1. **VS Code Dev Containers (`.devcontainer/`)**  
   - Interactive development inside VS Code  
   - Automatically installs PKL & Java  
   - Mounts your workspace for live edits

2. **Docker Compose Runtime (`docker-compose.yml`)**  
   - Run PKL evaluation from the command line  
   - Pass `.pkl` input and receive `.json` output  
   - No need for VS Code to be open

---

## 📦 Folder Structure

``` bash
.
├── .devcontainer
│ ├── Dockerfile
│ └── devcontainer.json
├── README.md
├── docker-compose.yml
└── src
  ├── example.pkl
  └── exampleBase.pkl
```


## 🚀 Running in VS Code Dev Containers

1. Install:
   - VS Code
   - Dev Containers extension
   - Docker Desktop

2. Open the project in VS Code.

3. When prompted, click:

   **“Reopen in Container”**
   
   OR 
   
   Press **F1 → Dev Containers: Reopen in Container**
   
   The container will build and start automatically.

4. You can now run PKL commands from the integrated terminal:

```bash
pkl eval src/example.pkl --format json
```

##  Running via Docker Compose

The Docker Compose setup lets you run PKL evaluations without VS Code.
Usage:

```bash
docker compose run pkl-runner -f json src/example.pkl > output.json
```


This generates:

> output.json

in the repository root.


# How It Works

The container ENTRYPOINT is pkl, so running the container is the same as running PKL.

`docker-compose.yml` mounts the `src/` directory and the current folder.

The PKL file path you pass is forwarded directly to PKL.

Example:
``` bash
docker compose run --rm pkl-runner src/example.pkl
```

Equivalent to:

```bash
pkl eval src/example.pkl --format json 
```

# Notes

`PKL 0.30.0` for Linux is installed directly from GitHub.

UID/GID problems on Windows/WSL are avoided by using
`"updateRemoteUserUID": true`.

`Java 21` is included per PKL requirements.

# Example PKL → JSON
```bash
docker compose run --rm pkl-runner src/example.pkl
```

Produces:
```json
{
  "sql_config": {
    ...
  }
}
```
