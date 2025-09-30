# 🚀 NoorAhmed DevOps Dashboard Project

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![GitHub last commit](https://img.shields.io/github/last-commit/NoorAhmed786/Devops)](https://github.com/NoorAhmed786/Devops/commits/main)
[![Issues](https://img.shields.io/github/issues/NoorAhmed786/Devops)](https://github.com/NoorAhmed786/Devops/issues)

---

## **Project Overview**

This project is a **multi-page dashboard website** deployed on Ubuntu using:

- Apache web server
- GitHub repository
- Jenkins CI/CD pipeline
- MySQL database (for future use)
- Password-less SSH for deployment

It demonstrates a **full DevOps workflow**: push code to GitHub → automatic build & deployment via Jenkins → live website updates.

---

## **Features**

- Multi-page dashboard:
  - `index.html` → Home / Dashboard
  - `projects.html` → Projects page
  - `services.html` → Services page
  - `team.html` → Team page
  - `contact.html` → Contact form
- Styled with `style.css`
- Automatic deployment via Jenkins pipeline
- Password-less SSH deployment
- Handles **additions, modifications, and deletions** automatically

---

## **Installation & Setup**

### **1. Install Apache Web Server**

```bash
sudo apt update
sudo apt install apache2 -y
sudo systemctl enable apache2
sudo systemctl start apache2
```

### **2. Configure Website Directory**

```bash
sudo mkdir -p /var/www/noor.com/public_html
sudo chown -R $USER:$USER /var/www/noor.com/public_html
```

### ***Create virtual host file:***
```bash
sudo nano /etc/apache2/sites-available/noor.com.conf
```
### ***Example content:***
```bash
<VirtualHost *:80>
    ServerAdmin admin@noor.com
    ServerName noor.com
    DocumentRoot /var/www/noor.com/public_html
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
### ***Enable the site and reload Apache:***
```bash
sudo a2ensite noor.com.conf
sudo systemctl reload apache2
sudo systemctl restart apache2
```

### **3. Install Git & Setup GitHub SSH Authenticationb**
#Install Git:
```bash
sudo apt install git -y
git --version
```
# Generate SSH key:
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```
# Copy key to remote Ubuntu server:
```bash
ssh-copy-id -i ~/.ssh/id_ed25519 vboxuser@192.168.56.105
```
# Test password-less SSH:
```bash
ssh -i ~/.ssh/id_ed25519 vboxuser@192.168.56.105
```
# Clone the GitHub repository:
```bash
git clone git@github.com:NoorAhmed786/Devops.git
cd Devops
```

### **4. Install & Secure MySQL**
Install MySQL:
```bash
sudo apt install mysql-server -y
sudo systemctl start mysql
sudo systemctl enable mysql
```
Secure MySQL installation:
```bash
sudo mysql_secure_installation
```
Follow prompts to:
 - Set root password
 - Remove anonymous users
 - Disallow remote root login
 - Remove test database

### **5. Install Jenkins**
Install OpenJDK:
```bash
sudo apt update
sudo apt install openjdk-11-jdk -y
```
Add Jenkins repository and key:
```bash
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update
```
Install Jenkins:
```bash
sudo apt install jenkins -y
sudo systemctl start jenkins
sudo systemctl enable jenkins
```
- Access Jenkins: `http://192.168.56.105:8080`

### **6. Connect Jenkins with GitHub**
1. Add SSH key in Jenkins:
  - Manage Jenkins → Manage Credentials → Global → Add Credentials
  - Kind: SSH Username with private key
  - Username: git
  - Private Key: /var/lib/jenkins/.ssh/id_ed25519
2. Create a Pipeline job using the repository and Jenkinsfile.

### **7. Jenkins Pipeline**
```bash
pipeline {
    agent any

    environment {
        DEV_SERVER_IP = '192.168.56.105'
        USERNAME = 'vboxuser'
        PRIVATE_KEY_PATH = '/var/lib/jenkins/.ssh/id_ed25519'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'git@github.com:NoorAhmed786/Devops.git',
                    credentialsId: 'GitHub SSH Key'
            }
        }

        stage('Build') {
            steps {
                sh 'echo "Build stage completed"'
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying all changes to ${DEV_SERVER_IP}..."
                sh """
                    rsync -avz --delete --exclude ".git/" \
                    -e "ssh -i ${PRIVATE_KEY_PATH} -o StrictHostKeyChecking=no" \
                    ${WORKSPACE}/ ${USERNAME}@${DEV_SERVER_IP}:/var/www/noor.com/public_html/
                """
            }
        }
    }
}
```
- This automatically deploys new files, updates, and deletes removed files.

### **8. Git Workflow**

1. Add new files:  
```bash
git add .
git commit -m "Add new files"
git push origin main
```
2. Modify or delete files:
```bash
git add -u
git commit -m "Update or delete files"
git push origin main
```
- Jenkins automatically deploys all changes including deletions.

 ### **10. Access Website**
 Visit:
 ```bash
http://`192.168.56.105`
```
- Multi-page dashboard should be live and fully functional.

 ### **9. Troubleshooting**
 | Issue                     | Cause                 | Solution                           |
|----------------------------|-----------------------|------------------------------------|
| Jenkins cannot clone repo  | Missing credentials   | Add SSH key in Jenkins             |
| Deployment fails           | SSH permissions       | Setup password-less SSH            |
| Deleted files not removed  | Rsync missing --delete| Add --delete option                |
| Git push fails             | Local behind remote   | Run `git pull origin main --rebase`|


### **11. Screenshots**

Place screenshots in a `folder screenshots/:`
```bash
### 1. Dashboard Website
![Dashboard](screenshots/dashboard.png)

### 2. Jenkins Pipeline Build
![Jenkins Build](screenshots/jenkins_build.png)

### 3. GitHub Repository
![GitHub Repo](screenshots/github_repo.png)

### 4. Deployment Workflow
![Deployment GIF](screenshots/deployment.gif)
```

### **12. Additional Tips for Students**

- Push changes to GitHub first; Jenkins handles deployment automatically.
- Use `git add -u` for modifications/deletions and `git add .` for new files.
- Test password-less SSH:
```bash
ssh -i ~/.ssh/id_ed25519 vboxuser@192.168.56.105

```






