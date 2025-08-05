# Flask To-Do App with Docker, Jenkins, and AWS EC2

A production-grade To-Do list application built with Flask and SQLite, containerized using Docker, and deployed on AWS EC2 with Jenkins CI/CD.

---

## Project Structure

```
todo_app/
├── app/
│   ├── __init__.py
│   ├── routes.py
│   ├── models.py
│   ├── templates/
│   └── static/
├── instance/
│   └── todo.db (auto-created)
├── config.py
├── run.py
├── requirements.txt
├── Dockerfile
├── Jenkinsfile

```

---

##  Features

- Add, complete, and delete tasks
- Flask web app with SQLite database
- Dockerized for deployment
- CI/CD using Jenkins
- Deployed on AWS EC2

---

##  Prerequisites

- AWS EC2 instance (Ubuntu 22.04 recommended)
- Docker installed on EC2 ✅
- Jenkins installed on EC2 ✅
- GitHub repository with project code
- Inbound ports open in EC2 security group:
  - Port 22 (SSH)
  - Port 5000 (Flask)
  - Port 8080 (Jenkins UI)

---

##  Local Development (Optional)

1. Clone the repository
2. (Optional) Create virtual environment
3. Install dependencies:
   ```
   pip install -r requirements.txt
   ```
4. Run the app:
   ```
   python run.py
   ```
5. App runs at `http://localhost:5000`

---

##  Docker Setup

1. Build Docker image:
   ```
   docker build -t todo-app .
   ```

2. Run the container:
   ```
   docker run -d -p 5000:5000 --name todo-container todo-app
   ```

3. App runs at `http://localhost:5000`

---

##  Jenkins + Docker on EC2

You’ve already installed Jenkins and Docker on your EC2 instance ✅

### Verify installations:

```bash
docker --version
sudo systemctl status jenkins
```

### Grant Jenkins access to Docker:

```bash
sudo usermod -aG docker jenkins
sudo chown jenkins:docker /var/run/docker.sock
sudo systemctl restart jenkins
```

---

##  Jenkins Pipeline Setup

### 1. Access Jenkins:
```
http://<EC2_PUBLIC_IP>:8080
```

### 2. Unlock Jenkins with initial password:
```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

### 3. Install suggested plugins and create admin user

### 4. Create a new pipeline job:
- Name: `todo-pipeline`
- Type: **Pipeline**
- Choose: **Pipeline script from SCM**
- Repository URL: your GitHub repo
- Script Path: `Jenkinsfile`

---

##  Jenkins Pipeline Stages (in Jenkinsfile)

- Clone your Flask project from GitHub
- Build Docker image
- Stop/remove existing container
- Run the new container

---

##  Access the App

Once Jenkins completes the build:

```
http://<EC2_PUBLIC_IP>:5000
```

---

##  Optional Enhancements

- Add Nginx reverse proxy to serve on port 80
- Enable HTTPS with Let's Encrypt
- Replace SQLite with PostgreSQL
- Use GitHub webhooks for auto-deployment
- Push Docker image to Amazon ECR or Docker Hub

---

---

##  Status

- [x] Flask app created
- [x] Dockerized
- [x] Jenkins installed on EC2
- [x] Docker installed on EC2
- [x] CI/CD pipeline built
- [x] Flask app deployed via Jenkins on EC2

