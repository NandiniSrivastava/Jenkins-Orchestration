# 🧪 Simple Python Application with Jenkins CI/CD Pipeline

## 📌 Project Overview

This project demonstrates a simple Python application integrated with a complete CI/CD pipeline using **Jenkins**, **Docker**, and **GitHub**.  
The application is a command-line tool that adds two numbers together. The project features:

- Automated testing
- Continuous Integration/Deployment using Jenkins
- Dockerized build and testing environments

> ⚠️ **Note**: Ensure Docker Desktop is running before executing any Docker-related commands.

---

## 🧩 Project Structure

```
.
├── sources/
│   ├── add2vals.py        # Main CLI application
│   ├── calc.py            # Core logic (addition)
│   └── test_calc.py       # Unit tests
├── dist/                  # Generated executables
├── requirements.txt       # Python dependencies
├── Jenkinsfile            # CI/CD pipeline configuration
├── docker-compose.yml     # Docker environment for Jenkins
└── README.md              # Project documentation
```

---

## 🐍 Python Application

- **`add2vals.py`**: Entry point that handles CLI input and displays results.
- **`calc.py`**: Contains the logic for adding two numbers.
- **`test_calc.py`**: Unit tests for the `calc` module.
- **`requirements.txt`**: Python packages required for the application.

---

## ⚙️ CI/CD Pipeline with Jenkins

### 🔧 Jenkins Configuration

- **Jenkinsfile**: Defines the CI/CD workflow (build, test, package).
- **docker-compose.yml**: Spins up Jenkins server and agent containers with required volumes and networks.

### 🐳 Docker Containers

- **Jenkins Server**: Main CI/CD orchestrator with persistent storage.
- **Jenkins Agent**: Handles builds and job execution.
- **Python Build Container**: Used to build and test the Python app.

---

## 🚀 Getting Started

### Step 1: Setup Jenkins

Start Jenkins using Docker Compose:
```bash
docker-compose up -d
```
![image](https://github.com/user-attachments/assets/8bb2d13a-f674-4474-9a44-2287da9a10ba)

Get the initial admin password:
```bash
docker-compose exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

Access Jenkins in your browser:  
`http://localhost:8080`

Complete the setup:
- Install suggested plugins
- Create the first admin user
- Keep the default Jenkins URL
![image](https://github.com/user-attachments/assets/969564bb-a606-460f-9925-08e1c299f7c0)

### Step 2: Create the Pipeline Project

1. Click **"New Item"**
2. Name the project: `simple-python-pyinstaller-app`
3. Choose **"Pipeline"**, click **OK**
4. Under **Pipeline script from SCM**:
   - SCM: `Git`
   - Branch: `*/master`

Click **Save**

![image](https://github.com/user-attachments/assets/aaa65a87-376e-4be5-9881-55cf91ff0ae2)
![image](https://github.com/user-attachments/assets/93d6690d-bef1-455a-9ab9-a052badd5e49)


### Step 3: Configure Docker Inside Jenkins

Install Docker inside Jenkins container:
```bash
docker-compose exec jenkins bash -c "apt-get update && apt-get install -y docker.io"
docker-compose exec jenkins bash -c "service docker start"
docker-compose exec jenkins docker --version
```
![Screenshot 2025-04-02 185509](https://github.com/user-attachments/assets/eae23ce2-d629-4c0c-a62a-7c77cf53f1a8)

![Screenshot 2025-04-02 185549](https://github.com/user-attachments/assets/4f4af70a-4e18-46c6-ba59-e2289466cd25)

![Screenshot 2025-04-02 185638](https://github.com/user-attachments/assets/c833c8ce-e700-4140-8bef-0921681cfbec)

Install required Docker plugins in Jenkins:
- Docker Pipeline
- Docker plugin
- docker-build-step
- 
![image](https://github.com/user-attachments/assets/9c9b3ac8-0bd8-4b21-9230-b365d3743f4d)
![image](https://github.com/user-attachments/assets/17c8de84-624b-4ace-972c-c26d0b047524)


Restart Jenkins:
```bash
docker-compose restart jenkins
```
![Screenshot 2025-04-02 190327](https://github.com/user-attachments/assets/96ae0671-5a33-43bc-ad48-b6d2a8fce765)

---
![image](https://github.com/user-attachments/assets/491db0ec-86ae-4a5a-a857-acdb9bf3723c)


## ▶️ Running the Pipeline

1. Go to the pipeline project in Jenkins
2. Click **"Build Now"**
![image](https://github.com/user-attachments/assets/a03ce130-60b4-4081-bb2e-672ad12cbb20)


4. After the build completes, download the executable from **Build Artifacts**

---

## 💻 Running the Executable

> The generated executable is a Linux binary.

To run on Windows, use **WSL** (Windows Subsystem for Linux):

### Setup WSL

```bash
wsl --version
# If WSL is not installed:
wsl --install
```

### Run the Executable in WSL

```bash
wsl
cd /mnt/c/Users/<your-user>/Downloads
chmod +x add2vals
./add2vals 5 3
```
![image](https://github.com/user-attachments/assets/27cb822a-b71e-43dd-8372-b86bb403d72f)


---

## 📦 What Does PyInstaller Do?

**PyInstaller** converts Python scripts into standalone executables.

### ✅ Process

- **Analysis**: Scans source files and dependencies
- **Bundling**: Packages everything including Python interpreter
- **Output**: Generates an executable in `dist/`

### ✅ Benefits

- **Portability**: Single-file executable
- **No Dependencies**: No need to install Python
- **Cross-Platform**: Works on Windows, Linux, macOS
- **Consistency**: Same behavior across environments

---

## ✅ Conclusion

This project showcases a complete CI/CD pipeline using:

- Jenkins for automation
- Docker for containerization
- PyInstaller for building portable executables

