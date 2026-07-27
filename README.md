# Parallel CI Pipeline & Distributed Build Architecture

## Problem Statement Overview
Running CI tasks sequentially (like testing and static analysis) significantly increases build times and slows down developer feedback. Furthermore, running all these resource-intensive builds on a single Jenkins server creates long build queues, resource limitations, and environments that are difficult to manage[cite: 1]. 

## Solution Approach
To solve these issues, the CI pipeline was optimized in two ways:
1. **Pipeline Level (Project 1.2):** Modified the `Jenkinsfile` to execute Unit Tests, Integration Tests, and Static Code Analysis concurrently using parallel stages to reduce overall execution time.
2. **Infrastructure Level (Project 1.3):** Implemented a Jenkins distributed build architecture. The Jenkins Controller (Master) was configured to manage pipeline configurations and job scheduling, while a dedicated Jenkins Agent was provisioned to execute the actual build tasks. 

## Dependencies and Tools
* Jenkins Controller (Master)
* Jenkins Agent (Node)
* GitHub & Git
* Java & Maven

## Execution Steps

### Part 1: Setting up the Master-Agent Architecture
1. **Agent Preparation:** Provisioned a secondary machine to act as the Jenkins agent and installed required dependencies: Java, Git, and Maven.
2. **Node Configuration:** Added a "New Node" in the Jenkins Controller named `agent-java-node` (Permanent Agent).
3. **Agent Settings:** Configured the Remote Root Directory to `/home/jenkins/agent` and assigned the label `java-agent`.
4. **Connection:** Connected the agent to the controller via SSH using the agent machine's IP address and SSH credentials.

### Part 2: Executing the Parallel Pipeline
1. **Job Assignment:** Configured the Jenkins Pipeline job to restrict where the project can run by specifying the `java-agent` label, ensuring builds run on the agent instead of the controller.
2. **Pipeline Execution:** Triggered the pipeline, which checks out the code, builds the application, and runs the parallel testing stages.
3. **Verification:** Monitored the Jenkins Stage View to verify parallel execution and checked the console logs to confirm the job was successfully executed on the distributed agent node.
