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
