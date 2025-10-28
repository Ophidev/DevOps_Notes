
# 🐳 Docker Swarm — Complete Notes

## 🚀 What is Docker Swarm?

Docker Swarm is a **container orchestration tool** built into Docker that helps you manage multiple containers across multiple machines (**a cluster**).

It allows you to: 

✅ Deploy containers across many nodes

✅ Automatically scale apps

✅ Load balance traffic

✅ Ensure high availability

✅ Monitor and self-heal services


---

## 🧠 Why Swarm? (Benefits)

✨ Deployment

📈 Auto-scaling

⚖️ Resource Allocation across cluster

🔁 Load Balancing

💓 Health Monitoring

🛡️ Fault Tolerance

---

## 🔹 Swarm Architecture Overview
![alt text](image.png)

📌 *Manager makes decisions*
📌 *Workers only execute containers given by manager*

---

## 📌 Important Terminology

| Term             | Meaning                                  | Emoji |
| ---------------- | ---------------------------------------- | ----- |
| **Node**         | A Docker host in the Swarm               | 🖥️   |
| **Manager Node** | Controls cluster, assigns tasks          | 👑    |
| **Worker Node**  | Runs containers assigned by manager      | 👷    |
| **Service**      | Defines how tasks should run (blueprint) | 🛠️   |
| **Task**         | Actual running container instance        | 📦    |
| **Swarm**        | Group of nodes working together          | ⚙️🔥  |

---

## 🧑‍💻 Practicing Docker Swarm on a Single Machine

Using **Docker-in-Docker** (dind) image to simulate multiple Linux hosts

### ✅ Step 1 — Create Nodes using Containerized Docker Engine

```sh
docker run --privileged -d --name manager docker:dind
docker run --privileged -d --name worker1 docker:dind
docker run --privileged -d --name worker2 docker:dind
docker run --privileged -d --name worker3 docker:dind
```

✅ `--privileged` → gives container kernel access
✅ `docker:dind` → Docker Engine running inside Docker

📌 Each container = one swarm node

---

### ✅ Step 2 — Initialize Swarm on Manager

```sh
docker exec -it manager sh
docker swarm init
```

This generates a join command like:

```
docker swarm join --token <token> <manager-ip>:2377
```

---

### ✅ Step 3 — Join Workers to Swarm

Run inside each worker:

```sh
docker exec -it worker1 sh
docker swarm join --token <token> <manager-ip>:2377
```

Repeat for worker2 + worker3 ✅

---

### ✅ Step 4 — Verify Swarm Cluster

Inside manager:

```sh
docker node ls
```

You should see 👑 manager + 3 workers

Example output:

```
ID HOSTNAME STATUS AVAILABILITY MANAGER STATUS
xx manager  Ready Active Leader 👑
yy worker1  Ready Active
zz worker2  Ready Active
aa worker3  Ready Active
```

---

## 🚀 Deploying a Service in Swarm

Example: Deploy 5 NGINX containers

```sh
docker service create --name webapp --replicas 5 -p 8080:80 nginx
```

List services:

```sh
docker service ls
```

Check where tasks are running:

```sh
docker service ps webapp
```

---
### ✅worker leaving swarm

```sh
docker swarm leave
# node left but the production code will be leave in the swarm only
```

Node left the swarm

---

### ✅ Scaling Changes in Production (1 Command!)

```sh
docker service scale webapp=10
```

Boom! ⚡ 5 more containers deployed automatically

---

### 🛑 Remove Service

```sh
docker service rm webapp
```

---

## ✅ Swarm Recap Table

| Feature             | Docker | Swarm |
| ------------------- | ------ | ----- |
| Single Machine      | ✅      | ✅     |
| Cluster of Machines | ❌      | ✅     |
| Auto Scaling        | ❌      | ✅     |
| Load Balancing      | ❌      | ✅     |
| Self-Healing        | ❌      | ✅     |

---

## 🎯 Final Summary

You have learned:
✅ What Swarm is
✅ Architecture (Manager + Workers)
✅ Services & Tasks
✅ Creating a Swarm cluster using Docker containers
✅ Deploy + Scale apps in the cluster

---

### 🔥 Next Step for You

✅ Deploy your MERN App in Swarm environment
✅ Add CI/CD Pipelines later (Jenkins)
✅ Then move to Kubernetes after strong Swarm basics
✅ Learn Helm afterward

---

