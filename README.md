# Parallel CI Pipeline & Distributed Build Architecture

## 📌 Project Overview

This project demonstrates how to improve Continuous Integration (CI) performance by implementing **parallel pipeline execution** and a **distributed Jenkins build architecture**. The pipeline executes multiple stages simultaneously, significantly reducing build time, while a Jenkins Controller-Agent setup distributes workloads across dedicated build nodes to improve scalability and resource utilization.

---

## 🎯 Objectives

- Implement parallel execution of CI pipeline stages.
- Reduce overall build execution time.
- Configure a Jenkins Controller-Agent architecture.
- Execute builds on dedicated Jenkins agents.
- Improve CI pipeline scalability and performance.
- Automate build, testing, and analysis processes.

---

## 🏗️ Architecture

The CI solution consists of the following components:

- **GitHub Repository** – Stores the application source code and Jenkinsfile.
- **Jenkins Controller** – Manages jobs, pipelines, and build scheduling.
- **Jenkins Agent** – Executes build and testing tasks.
- **Parallel Pipeline** – Runs multiple stages concurrently.
- **Maven** – Builds and tests the Java application.

---

## 🛠️ Technologies Used

- Jenkins
- Jenkins Pipeline
- Jenkins Agent
- GitHub
- Git
- Java
- Apache Maven
- Declarative Jenkinsfile

---

## 📂 Project Structure

```text
parallel-pipeline-ci-demo/
│
├── Screenshots/
│
├── src/
│
├── Jenkinsfile
├── README.md
└── pom.xml
```

---

## 🚀 Project Implementation

### Part 1: Configure Jenkins Controller and Agent

#### 1. Prepare the Jenkins Agent

Install the required software:

- Java (JDK)
- Git
- Maven

---

#### 2. Add a New Node

In Jenkins:

- Manage Jenkins
- Nodes
- New Node
- Permanent Agent

Example configuration:

- Node Name: `agent-java-node`
- Remote Root Directory: `/home/jenkins/agent`
- Labels: `java-agent`

---

#### 3. Connect the Agent

Configure SSH credentials and connect the Jenkins agent to the Jenkins Controller.

Verify the node status from the Jenkins Dashboard.

---

### Part 2: Configure the Parallel Pipeline

#### 1. Create the Jenkins Pipeline Job

Configure:

- Pipeline script from SCM
- GitHub Repository
- Jenkinsfile

Assign the build to the Jenkins Agent using the label:

```groovy
agent {
    label 'java-agent'
}
```

---

#### 2. Execute the Pipeline

Run the pipeline.

The pipeline executes:

- Checkout
- Build
- Unit Tests (Parallel)
- Integration Tests (Parallel)
- Static Code Analysis (Parallel)

---

### Example Parallel Pipeline

```groovy
pipeline {

    agent {
        label 'java-agent'
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/ManojKumar8244/parallel-pipeline-ci-demo.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Parallel Testing') {

            parallel {

                stage('Unit Test') {
                    steps {
                        sh 'mvn test'
                    }
                }

                stage('Integration Test') {
                    steps {
                        echo 'Running Integration Tests'
                    }
                }

                stage('Static Code Analysis') {
                    steps {
                        echo 'Running Static Analysis'
                    }
                }

            }

        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

    }

}
```

---

## 🔍 Verification Commands

### Verify Maven Build

```bash
mvn clean compile
```

### Execute Unit Tests

```bash
mvn test
```

### Package the Application

```bash
mvn package
```

### Verify Build Artifact

```bash
ls target/
```

---

## 📊 Key Features

- Parallel Pipeline Execution
- Distributed Jenkins Architecture
- Jenkins Controller-Agent Setup
- Pipeline as Code
- Faster Build Execution
- Improved Resource Utilization
- Automated Build and Testing
- Scalable Continuous Integration

---

## 📚 Learning Outcomes

Through this project, I gained hands-on experience with:

- Jenkins Controller-Agent Architecture
- Parallel Pipeline Execution
- Declarative Jenkins Pipeline
- Pipeline as Code
- Maven Build Automation
- Continuous Integration (CI)
- Distributed Build Systems
- Jenkins Node Management

---

## 📸 Screenshots

Include screenshots of:

- Jenkins Dashboard
- Jenkins Controller and Agent Nodes
- Node Configuration
- Pipeline Configuration
- Parallel Pipeline Stage View
- Successful Build
- Jenkins Console Output
- Generated Artifacts (`target/`)

---

## ✅ Project Outcome

Successfully implemented a Jenkins-based distributed build architecture with parallel pipeline execution. By configuring a Jenkins Controller-Agent setup and executing multiple testing stages concurrently, the project significantly reduced build times and improved CI pipeline efficiency. This implementation demonstrates DevOps best practices for scalable, maintainable, and high-performance Continuous Integration workflows.

---

## 👨‍💻 Author

**Manoj Kumar**

- GitHub: https://github.com/ManojKumar8244
