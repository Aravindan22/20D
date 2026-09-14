# 20-Day Lock-In Plan
**SSE · 5 YOE Python Backend · ~2 hrs/day after office**

Topics: Docker · Golang · RabbitMQ · Kubernetes · FastMCP

### Ground Rules (realistic version)
- Most days touch **2–3 topics** (one main focus + light practice/review on others).
- “Must-do” = the core hands-on. Do this even on low-energy days.
- “Stretch” = extra practice or polish. Skip freely.
- Keep **one single Git repo**. Folders: `docker/`, `golang/`, `rabbitmq/`, `k8s/`, `fastmcp/`, `combined/`.
- 5–10 min flashcard review at the start of almost every session.
- Some days you’ll do 45–60 min, some 3 hrs. Both are fine. Just don’t break the streak completely.

### Flashcards
Use Anki or a simple Markdown file. Review 5–10 min daily.
High-value cards are listed under each topic. Keep the deck small.

---

## Week 1 (Days 1–7) — Foundations + Early Wins

### Day 1
**Primary: Docker**  
**Secondary: Golang (just setup)**

Must-do:
- Install Docker Desktop / Engine
- Run a few official images, inspect, exec into them
- Write a simple Dockerfile for a tiny Python FastAPI/Flask app you already know
- Build & run it

Stretch:
- Add a .dockerignore and multi-stage build skeleton

Golang stretch:
- Install Go, set up GOPATH/modules, run `hello world`

Flashcards start:
- What is an image vs container?
- What does `docker run -it --rm` do?

### Day 2
**Primary: Docker**  
**Secondary: Golang**

Must-do:
- Volumes + bind mounts
- Networks (bridge)
- docker-compose.yml with your Python app + a simple Redis or Postgres

Golang:
- Basic syntax, variables, structs, error handling (`if err != nil`)
- Write 2–3 tiny CLI programs

Flashcards:
- Difference between VOLUME and bind mount
- When to use multi-stage builds

### Day 3
**Primary: Golang**  
**Secondary: Docker**

Must-do (Go):
- HTTP server with `net/http` or Gin/Fiber
- JSON encode/decode
- Simple REST endpoints

Docker practice:
- Dockerize the Go hello/http service you just wrote
- Compare image size with your Python one

### Day 4
**Primary: Docker + Golang together**  
**Secondary: light RabbitMQ intro**

Must-do:
- Multi-stage Go Dockerfile (tiny final image)
- docker-compose with Python service + Go service talking over a network

RabbitMQ stretch:
- Spin up RabbitMQ with Docker (`rabbitmq:3-management`)
- Open the management UI, create a queue manually

Capstone-ish:
- Both services running via compose and can curl each other

### Day 5
**Primary: Golang**  
**Secondary: RabbitMQ (Python side)**

Must-do (Go):
- Goroutines + channels
- Simple worker pool pattern

RabbitMQ:
- Python producer & consumer (pika or aio-pika)
- Basic work queue: send tasks, consume them

Flashcards:
- Goroutine vs thread
- What is an exchange vs a queue?

### Day 6
**Primary: RabbitMQ**  
**Secondary: Golang + Docker**

Must-do:
- Exchanges, routing keys, bindings
- Durable queues + persistent messages
- Acknowledgments & basic error handling

Go practice:
- Write a simple Go consumer for the same queue

Docker:
- Add RabbitMQ to your existing docker-compose and make the services use it

### Day 7
**Primary: RabbitMQ + Golang**  
**Secondary: Docker polish**

Must-do:
- Capstone mini: Python producer → RabbitMQ → Go consumer that does some work (e.g. process a job, write result somewhere)
- Everything runs via docker-compose

Stretch:
- Dead-letter queue basic setup
- Proper logging and graceful shutdown in Go

---

## Week 2 (Days 8–14) — Messaging Deep Dive + Kubernetes Entry

### Day 8
**Primary: Kubernetes (local setup)**  
**Secondary: Docker + RabbitMQ review**

Must-do:
- Install kind / k3d / minikube (pick the lightest for your machine)
- First pod, deployment, service
- Deploy one of your existing Docker images

Flashcards:
- Pod vs Deployment vs Service
- What is a label selector?

### Day 9
**Primary: Kubernetes**  
**Secondary: Golang**

Must-do:
- ConfigMaps + Secrets
- Resource requests/limits
- Liveness & readiness probes
- Deploy your Go service to local K8s

Go stretch:
- Add a simple health endpoint if you don’t have one

### Day 10
**Primary: Kubernetes + RabbitMQ**  
**Secondary: Docker**

Must-do:
- Deploy RabbitMQ to local K8s (or use a simple Helm chart / official manifests)
- Make your Python + Go services talk to it inside the cluster
- Service discovery via DNS names

### Day 11
**Primary: Golang**  
**Secondary: Kubernetes**

Must-do (Go):
- Better error handling, context package
- Basic testing (`testing` package)
- Improve the consumer from earlier days

K8s practice:
- Rolling update of your Go deployment
- Scale it up/down and watch

### Day 12
**Primary: RabbitMQ patterns**  
**Secondary: Kubernetes**

Must-do:
- Pub/Sub pattern
- Topic exchange or headers if you want
- Retry + dead-letter more carefully

K8s:
- Add horizontal pod autoscaler (basic) or just practice scaling

### Day 13
**Primary: Kubernetes**  
**Secondary: FastMCP intro**

Must-do:
- Volumes / PersistentVolumeClaims (simple)
- Ingress (if your local setup supports it easily) or just port-forward
- Clean up and document your current K8s manifests

FastMCP stretch:
- Install FastMCP
- Run the official quickstart (tiny tool server)

### Day 14
**Primary: FastMCP**  
**Secondary: Kubernetes + Docker**

Must-do:
- Build a small FastMCP server with 3–4 useful tools (can wrap existing logic or talk to RabbitMQ)
- Run it both via stdio and HTTP transport
- Dockerize the FastMCP server

---

## Week 3 (Days 15–20) — Integration + Capstone

### Day 15
**Primary: FastMCP + RabbitMQ**  
**Secondary: Golang**

Must-do:
- FastMCP tools that publish messages to RabbitMQ
- Or tools that query status of jobs
- Keep the Go consumer alive

### Day 16
**Primary: Kubernetes**  
**Secondary: FastMCP**

Must-do:
- Deploy the FastMCP server to local K8s
- Make sure it can reach RabbitMQ and any other services
- Test calling the tools from a client

### Day 17
**Primary: Combined system design**  
**Secondary: all previous**

Must-do:
- Sketch the final architecture on paper / in a README
- Decide what the combined project will do (keep it small)

Suggested combined idea:
- User/API triggers a job via FastMCP tool
- Job goes into RabbitMQ
- Go workers process it
- Results stored somewhere simple (file, Redis, or Postgres)
- Everything runs on local Kubernetes
- Bonus: FastMCP also exposes a tool to check job status

### Day 18
**Primary: Combined implementation**  
**Secondary: polish**

Must-do:
- Wire the pieces together
- Get the happy path working end-to-end
- Docker images + K8s manifests in the `combined/` folder

### Day 19
**Primary: Combined polish + testing**  
**Secondary: flashcards & notes**

Must-do:
- Handle a couple of failure cases (RabbitMQ down, worker crash, etc.)
- Add basic logging
- Write a short README explaining how to run the whole thing
- Heavy flashcard review of everything

### Day 20
**Primary: Final review + demo**  
**Secondary: whatever still feels weak**

Must-do:
- Run the full combined system from scratch
- Record a short Loom or just take screenshots/notes of it working
- Update flashcards with anything you still mix up
- Write 5–10 bullet “what I can now do” list for yourself

Stretch:
- Clean up the repo so it’s presentable
- Optional: try the same stack on a free cloud K8s (if energy allows)

---

## High-Value Flashcard Themes (keep the deck lean)

**Docker**
- Image vs container
- Multi-stage builds – why and how
- Volumes vs bind mounts
- docker-compose networking basics
- Healthchecks

**Golang**
- Error handling pattern
- Goroutines + channels (when to use select)
- Interfaces (implicit)
- Modules & go.mod
- Context package basics

**RabbitMQ**
- Queue vs Exchange
- Work queue vs Pub/Sub
- Acknowledgments & durability
- Dead-letter queues
- Connection vs channel

**Kubernetes**
- Pod / Deployment / Service
- Labels & selectors
- ConfigMap vs Secret
- Probes (liveness vs readiness)
- Service discovery inside the cluster

**FastMCP**
- What MCP is (one sentence)
- `@mcp.tool` decorator
- stdio vs HTTP transport
- How a client calls a tool
- When you’d use FastMCP vs a normal API

---

## Final Notes
- The goal is **working muscle memory**, not perfection.
- If a day goes sideways, just do the Must-do of the primary topic and one flashcard review. That still counts.
- When you finish Day 20 you’ll have:
  - Multiple small projects
  - One combined system that uses almost everything
  - A personal flashcard deck
  - Real confidence that you can spin these up at work

You’ve got this. Start Day 1 whenever you’re ready and just keep the streak alive.

Repo suggestion structure:
```
lock-in-20/
├── docker/
├── golang/
├── rabbitmq/
├── k8s/
├── fastmcp/
├── combined/
├── flashcards/
└── 20-day-lock-in-plan.md   ← this file
```
