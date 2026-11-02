# DevOps Practice Lab

A six-phase DevOps project covering application development, containerization, CI/CD, Infrastructure as Code, and monitoring, built on a Linux VM.

## Technologies

Python, Flask, Pytest, Git/GitHub, Docker, Docker Compose, Docker Hub, Jenkins, GitHub Actions, Terraform, Prometheus, Node Exporter, cAdvisor, Alertmanager, Grafana, stress-ng, Linux, firewalld

## Phases

**1. Application and testing**
Flask app with `/`, `/health` and `/version` endpoints, Pytest tests, and a Git workflow with `develop` and `main` branches, a merge conflict resolved, and tag `v1.0.0`.

**2. Docker**
Multi-stage Dockerfile, container run on host port 5002, Redis container on a custom network.

**3. Jenkins**
Declarative pipeline (Checkout, Build, Test) triggered automatically by a GitHub webhook.

**4. GitHub Actions**
Pytest on Python 3.10 and 3.12, then the image is built and pushed to Docker Hub on pushes to `main`, using repository secrets.

**5. Terraform**
Modular config managing an nginx container, network, and volume. Full plan, apply, and destroy lifecycle. Changing the host port from 8081 to 8082 forced a resource replacement.

**6. Monitoring**
Prometheus, Node Exporter, cAdvisor, Alertmanager and Grafana in Docker Compose. A `HighCPUUsage` alert was tested with stress-ng, and a Grafana dashboard shows CPU, memory, and container count.

## Docker Image

Docker Hub: `mhdsanjid/devops-mastery-app`

## Run Locally

```bash
pip install -r requirements.txt
pytest -v
docker build -t devops-app:1.0 .
docker run -d --name devops-app -p 5002:5000 devops-app:1.0
```

Monitoring stack:
```bash
cd phase6
docker compose up -d
```

> The Grafana `admin/admin` login is a default for local lab use only.

## Full Report

The complete walkthrough with configuration files, command logs, and screenshots is in [DEVOPS_PRACTICAL_LAB.pdf](DEVOPS_PRACTICAL_LAB.pdf).

## Author

Mohammed Sanjid, Cloud & DevOps Trainee
