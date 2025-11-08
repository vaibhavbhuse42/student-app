# 🧑‍💻 Student-App – Java CI/CD Pipeline using Jenkins & Tomcat on AWS EC2

## 📘 Project Overview
This project demonstrates a **CI/CD pipeline** for a Java-based web application named **Student-App**.  
It automates the build, test, and deployment process using **Jenkins**, **Maven**, and **Apache Tomcat** running on an **AWS EC2 instance**.

---

## 🚀 Tech Stack

| Component | Technology Used |
|------------|-----------------|
| **Backend** | Java (Maven Project) |
| **Build Tool** | Apache Maven |
| **Server** | Apache Tomcat 9 |
| **CI/CD Tool** | Jenkins |
| **Hosting Platform** | AWS EC2 (Ubuntu Instance) |
| **Version Control** | Git & GitHub |

---

## 🏗️ Project Setup Steps

### 1️⃣ Launch EC2 Instance
- Create an **Ubuntu EC2 instance** on AWS.
- Allow inbound rules for:
  - Port **22 (SSH)**
  - Port **8080 (Tomcat)**
  - Port **8081 (Jenkins)**

### 2️⃣ Install Required Packages
SSH into your EC2 instance and run:

```bash
sudo apt update
sudo apt install openjdk-17-jdk -y
sudo apt install maven -y
sudo apt install tomcat9 tomcat9-admin -y

```
## 3️⃣ Setup Jenkins

```bash
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian/ stable main > /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt install jenkins -y
sudo systemctl start jenkins
sudo systemctl enable jenkins

```
#### Access Jenkins at:
👉 http://<your-ec2-ip>:8081

## 🔐 Jenkins Configuration
### ➤ Add Credentials

Go to Manage Jenkins → Credentials → Global → Add Credentials

Kind: SSH Username with Private Key

ID: tomcat-key

Username: ubuntu

Private Key: paste your .pem key

### ➤ Configure Tools

Install Maven under “Global Tool Configuration”.

Install Git plugin.

## 🧩 GitHub Setup

Create a repository named student-app

Push your Java Maven code to it
#### Example:
```bash
git remote add origin https://github.com/vaibhavbhuse42/student-app.git
git push -u origin main

```
## 🧱 Jenkins Job Setup
### ➤ Create a Freestyle Project

#### Name: 
student-app-deployment

#### Source Code Management:

    Git URL: https://github.com/vaibhavbhuse42/student-app.git

#### Build Environment:
    Add Maven build step: clean install

#### Post-build Action:

    1.Deploy war to container

    2.WAR/EAR files: **/*.war

    3.Context path: /student-app

    4.Tomcat URL: http://<EC2-IP>:8080

    5.Credentials: use the tomcat-key

## 🧰 Deployment Process
#### 1>. Jenkins Pipeline Execution

     Click Build Now in Jenkins

#### 2>. Jenkins will:

     Pull code from GitHub

     Build WAR using Maven

     Deploy it automatically to Tomcat

## 🌐 Verify Deployment

#### Open in browser:
```bash
http://<EC2-IP>:8080/student-app

```
If everything is correct, your Java web application will be live! 🚀

## 🏗️ Architecture Diagram

![](/image/javaa%20A%20digram.webp)

### 📊 CI/CD Architecture Flow
![](/image/CICD%20pipline%20flow.png)
```bash
┌──────────────────────────┐
│        Developer         │
│ (Push Code to GitHub)    │
└────────────┬─────────────┘
             │
             ▼
┌──────────────────────────┐
│         Jenkins          │
│ (CI/CD Server on EC2)    │
│ - Pulls code from GitHub │
│ - Builds using Maven     │
│ - Deploys WAR to Tomcat  │
└────────────┬─────────────┘
             │
             ▼
┌──────────────────────────┐
│        Tomcat Server     │
│ (Running on EC2)         │
│ - Hosts Java WAR file    │
│ - Accessible via :8080   │
└────────────┬─────────────┘
             │
             ▼
┌──────────────────────────┐
│        End User          │
│ Access via Web Browser   │
│  http://<EC2-IP>:8080    │
└──────────────────────────┘

```
## 📸 Screenshots
### 🖥️ 1. Jenkins Dashboard

![](/image/Screenshot%20(31).png)

### ⚙️ 2. Build Console Output

![](/image/Screenshot%20(32).png)

### 🧾 3. Deployed Application on Tomcat

![](/image/Screenshot%20(33).png)

(Create a screenshots/ folder in your repo and upload these images)

## ✅ Project Highlights

Fully automated Java deployment pipeline

Integrated Jenkins with Tomcat via credentials

Maven build automation

Hosted securely on AWS EC2

Continuous Integration & Continuous Deployment implemented successfully

## 🧠 Conclusion

The Student-App CI/CD Pipeline Project successfully demonstrates how to automate the software delivery process for a Java web application using Jenkins, Maven, Tomcat, and AWS EC2.
This setup ensures:

Faster and more reliable deployments

Reduced manual errors

Continuous Integration & Continuous Delivery in a real-world environment

Through this project, we learn how DevOps tools work together to achieve end-to-end automation from code commit to deployment.

### 👨‍💻 Author

#### Vaibhav Navnath Bhuse
📧 vaibhavbhuse42@gmail.com

💼 GitHub Profile


