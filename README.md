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

### Step 2: Create the Pipeline Project

1. Click **"New Item"**
2. Name the project: `simple-python-pyinstaller-app`
3. Choose **"Pipeline"**, click **OK**
4. Under **Pipeline script from SCM**:
   - SCM: `Git`
   - Repository URL: `https://github.com/TarakKatoch/Jenkins-Orchestration.git`
   - Branch: `*/master`

Click **Save**

![Screenshot 2025-04-02 170804](https://github.com/user-attachments/assets/bda26b62-0620-46b4-8200-45f2c178bdd8)

![Screenshot 2025-04-02 185027](https://github.com/user-attachments/assets/3a3e6fc0-6492-4f78-80a7-7b351d438921)

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
![Screenshot 2025-04-02 185851](https://github.com/user-attachments/assets/c9b1a349-6284-4a1d-84aa-8b3173b73b27)

![Screenshot 2025-04-02 190119](https://github.com/user-attachments/assets/447d282b-e7eb-4999-adf5-751a6330b967)

![Screenshot 2025-04-02 190212](https://github.com/user-attachments/assets/e91f7d3d-7b47-4f2d-9944-9a3e537a5b0d)

Restart Jenkins:
```bash
docker-compose restart jenkins
```
![Screenshot 2025-04-02 190327](https://github.com/user-attachments/assets/96ae0671-5a33-43bc-ad48-b6d2a8fce765)

---
![Screenshot 2025-04-02 190405](https://github.com/user-attachments/assets/404e0fa0-18f8-49f6-9535-88fab0f541ee)


## ▶️ Running the Pipeline

1. Go to the pipeline project in Jenkins
2. Click **"Build Now"**
![Screenshot 2025-04-02 190919](https://github.com/user-attachments/assets/711869ef-5283-451d-9d06-61b3863ada3a)

![Screenshot 2025-04-02 190928](https://github.com/user-attachments/assets/5c760bad-8549-4d44-bd2f-6843261255d1)

![Screenshot 2025-04-02 190949](https://github.com/user-attachments/assets/84bd4d74-95f4-4866-93f3-10b5b1881f9a)

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
![Screenshot 2025-04-02 192308](https://github.com/user-attachments/assets/dc8022f0-a37f-4cda-8074-c67e98050b41)

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

### 💡 What You’ve Learned

- How to set up a Jenkins server with Docker
- How to automate build, test, and deployment pipelines
- How to use PyInstaller to package Python apps

---

## 🙌 Thank You!

If you found this helpful:

- ⭐ Star this repo
- 🔁 Share with others
- 🛠️ Contribute improvements or suggestions
- 🐞 Report any issues

**Happy Coding! 🚀**
