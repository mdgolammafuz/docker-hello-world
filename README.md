# Docker Hello World (CTO-Mode Crash Course)

This guide explains the **Dockerfile**, basic `docker` commands, and key concepts like image, container, host, port, and IP — tailored for our `hello-world-docker` FastAPI example.

---

## Folder Structure

```
hello-world-docker/
├── Dockerfile
├── requirements.txt
└── app/
    └── main.py
```

---

## Dockerfile: Explained Line-by-Line

```Dockerfile
# Base image with Python preinstalled
FROM python:3.10

# Set the working directory inside the container
WORKDIR /app

# Copy the requirements.txt to install dependencies
COPY requirements.txt .

# Install Python packages
RUN pip install -r requirements.txt

# Copy FastAPI app files into the container
COPY app/ .

# Command to run when the container starts
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

### What Each Line Does

- `FROM python:3.10`: Base image with Python pre-installed.
- `WORKDIR /app`: All following commands are run from this directory.
- `COPY requirements.txt .`: Copies dependency file into container.
- `RUN pip install -r requirements.txt`: Installs FastAPI and dependencies.
- `COPY app/ .`: Copies the `main.py` (and any other app files) into `/app`.
- `CMD [...]`: Runs the FastAPI server.

---

## Build the Docker Image

```bash
docker build -t hello-docker .
```

- `-t hello-docker`: Tags the image as `hello-docker`
- `.`: Builds from the current directory (Dockerfile location)

---

## Run the Container

```bash
docker run -p 8000:8000 hello-docker
```

- `-p 8000:8000`: Maps container port `8000` to host port `8000`
- Now access the API via: [http://localhost:8000](http://localhost:8000)

---

## Understanding Host, Port, and IP

| Term         | Meaning |
|--------------|---------|
| `host`       | Your physical/local machine |
| `container`  | Isolated mini-VM running your app |
| `--host 0.0.0.0` | Exposes the app on all available interfaces (so Docker can access it) |
| `localhost`  | Alias for `127.0.0.1` (your local machine) |
| `port`       | A communication endpoint (e.g., 8000) |

---

## 🧪 Verifying It Works

Once the container is running, open:

```
http://localhost:8000
http://localhost:8000/docs   ← Swagger UI
```

If it shows the FastAPI UI, we’ve succeeded!

---

## ✅ Summary

- We’ve built a FastAPI app inside Docker.
- We understand the role of image, container, host, port, and IP.
