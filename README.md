# DevOps Lab Exercises

Hands-on solutions to the ten exercises of the **DevOps Lab Manual** by Sunag P ([SunagP/DevOps-Lab](https://github.com/SunagP/DevOps-Lab/tree/main/Exercises)), completed for the DevOps course (21IS7PEDVR).

## Student Details

| Field | Details |
|---|---|
| Name | Kisha Khurana |
| USN | 1BM23IS125 |
| Branch | Information Science & Engineering |
| College | BMS College of Engineering, Bengaluru |
| Course | DevOps (21IS7PEDVR), 7th semester |

## About This Repository

The lab manual describes each exercise as a guide in `Exercises/`. This repository follows the same ten exercises, in the same order and with matching names. Each exercise has its own folder with:

- the **code and configuration files** from the manual (Python apps, Dockerfiles, Kubernetes YAML, Jenkinsfiles, scripts),
- a **README** with the objective, the commands that were run, and a screenshot of every step,
- a **Comparison with the Lab Manual** section listing every place where the manual's instructions had to change, and why.

Everything was run on a **MacBook Air (Apple Silicon) with macOS and Docker Desktop**, not on the Linux or WSL setup the manual assumes.

## Exercises

| # | Exercise | Folder | Manual |
|---|---|---|---|
| 1 | Kubernetes Getting Started: Hello Pod | [01-Kubernetes-Getting-Started](01-Kubernetes-Getting-Started) | [1-Kubernetes-Getting-Started.md](https://github.com/SunagP/DevOps-Lab/blob/main/Exercises/1-Kubernetes-Getting-Started.md) |
| 2 | Deploy a Flask app on Minikube using kubectl and YAML | [02-Minikube-Kubectl-Flask](02-Minikube-Kubectl-Flask) | [2-Minikube-Kubectl-Flask.md](https://github.com/SunagP/DevOps-Lab/blob/main/Exercises/2-Minikube-Kubectl-Flask.md) |
| 3 | Scaling a Flask app on a single node with ReplicaSets | [03-Minikube-Scaling-ReplicaSets](03-Minikube-Scaling-ReplicaSets) | [3-Minikube-Scaling-Flask-App-with-Replicasets.md](https://github.com/SunagP/DevOps-Lab/blob/main/Exercises/3-Minikube-Scaling-Flask-App-with-Replicasets.md) |
| 4 | Docker networking with multiple containers | [04-Docker-Networking](04-Docker-Networking) | [4-Docker-Networking.md](https://github.com/SunagP/DevOps-Lab/blob/main/Exercises/4-Docker-Networking.md) |
| 5 | Docker security with AppArmor and Python | [05-Docker-Security-AppArmor](05-Docker-Security-AppArmor) | [5-Docker-Security-AppArmor.md](https://github.com/SunagP/DevOps-Lab/blob/main/Exercises/5-Docker-Security-AppArmor.md) |
| 6 | Real-time monitoring and alerting (Prometheus, Grafana, Jenkins) | [06-Grafana-Prometheus-Monitoring](06-Grafana-Prometheus-Monitoring) | [6-Grafana-Realtime-Monitoring-of-Quick-Commerce-App.md](https://github.com/SunagP/DevOps-Lab/blob/main/Exercises/6-Grafana-Realtime-Monitoring-of-Quick-Commerce-App.md) |
| 7 | Introduction to CI and Jenkins installation | [07-Jenkins-CI-Automation](07-Jenkins-CI-Automation) | [7-Jenkins-CI-Automation.md](https://github.com/SunagP/DevOps-Lab/blob/main/Exercises/7-Jenkins-CI-Automation.md) |
| 8 | Creating a "Hello World" Jenkins job | [08-Jenkins-Hello-World-Job](08-Jenkins-Hello-World-Job) | [8-Jenkins-Hello-World-Job.md](https://github.com/SunagP/DevOps-Lab/blob/main/Exercises/8-Jenkins-Hello-World-Job.md) |
| 9 | Jenkins multi-stage pipeline for a Python application | [09-Jenkins-Multi-Stage-Pipeline](09-Jenkins-Multi-Stage-Pipeline) | [9-Jenkins-Multi-Stage-Pipeline.md](https://github.com/SunagP/DevOps-Lab/blob/main/Exercises/9-Jenkins-Multi-Stage-Pipeline.md) |
| 10 | Multi-node Kubernetes cluster with multiple applications | [10-Minikube-Multi-Node-Multi-App](10-Minikube-Multi-Node-Multi-App) | [10-Minikube-Multi-Node-Multi-App-Minikube-Deployment.md](https://github.com/SunagP/DevOps-Lab/blob/main/Exercises/10-Minikube-Multi-Node-Multi-App-Minikube-Deployment.md) |

## Comparison with Sunag's Repository

| | Sunag's repository | This repository |
|---|---|---|
| Exercises | 10 guides in `Exercises/` | the same 10 exercises, one folder each, same order |
| Format | one Markdown guide per exercise | a folder per exercise with code files, README and screenshots |
| Code | shown inside the guides | saved as real, runnable files, copied from the guides |
| Output shown | sample output from Linux or WSL | screenshots of the actual runs on macOS |
| Fixes to the guides | none listed | listed in each README's "Comparison with the Lab Manual" table |
| Other folders (Notes, Assignments, References, Syllabus, Images) | present | not copied; this repository covers the exercises only |

### Where the manual had to be changed

The code is the manual's code. These are the only changes, each explained in the exercise README:

| Exercise | Change | Reason |
|---|---|---|
| 1 | installed `kubectl` with Homebrew; `minikube start --driver=docker` | the manual lists only Minikube and no driver was auto-detected |
| 2, 3, 10 | `--container-runtime=docker` on `minikube start` | Minikube v1.39 defaults to containerd, where `minikube docker-env` fails |
| 3 | Dockerfile copies `app.py`; image `flashsale:1.0`; scale `flashsale-rs`; build before apply; no Docker Hub push | the manual's file, image and ReplicaSet names do not match each other |
| 4 | `host='0.0.0.0'`, pinned Werkzeug, MySQL root password, `ping` installed | needed for port publishing, a working Flask 2.0.1 image, MySQL startup and the connectivity test |
| 5 | AppArmor not enforced on macOS (exit codes 0 and 0 instead of 1 and 126) | Docker Desktop's Linux VM has no AppArmor; documented honestly |
| 6 | `host.docker.internal`, `-p 9090:9090`, 5-second intervals, added `Dockerfile`, adapted Jenkinsfile | the manual assumes Linux host networking and a Jenkins on the host |
| 7 | Jenkins run as root with the Docker socket and Docker CLI | lets the pipeline in Exercise 6 run Docker commands |
| 8, 9 | Jenkins branch `*/main`; Debian package names for Python | Jenkins defaults to `master`; the Jenkins image uses newer Python packages |
| 10 | `namespace: default` for the shopping cart; no `--force`; 2 GB per node | the manual never creates `devops-exercise`; `--force` is only for root |

## Companion Repository

Exercises 8 and 9 need Jenkins to pull code from GitHub, as the manual asks, so that code is in a second public repository:
**[khuranakisha/devops-sample-code](https://github.com/khuranakisha/devops-sample-code)** (`hello-world.sh`, `app.py`, `test_app.py`, `requirements.txt`, `Jenkinsfile`). Copies are also kept in folders 08 and 09 here.

## Environment

| Tool | Version |
|---|---|
| OS | macOS (Apple Silicon, arm64) |
| Docker Desktop | Docker 29.9.2 |
| Minikube | v1.39.0 (Docker driver) |
| kubectl | v1.37.1 |
| Kubernetes | v1.37.0 |
| Jenkins | 2.580.1 (`jenkins/jenkins:lts` in Docker) |

## Tools Used

Docker, Kubernetes (Minikube, kubectl), Jenkins, Prometheus, Grafana, AppArmor, Python, Flask, MySQL, Redis, Git, GitHub
