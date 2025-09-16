# Cyber Security Internship - Task 4: Linux Server Hardening

## Project Overview

This repository contains the deliverables for **Task 4** of the Cyber Security Internship. The project's main objective was to gain hands-on experience in **Linux server hardening**, a critical security practice focused on reducing a system's attack surface and mitigating vulnerabilities.

***

## Tools Used 🛠️

* **Kali Linux:** The operating system used for both the client and server roles.
* **SSH (Secure Shell):** The protocol for secure remote management.
* **UFW (Uncomplicated Firewall):** A user-friendly front-end for `iptables` that manages firewall rules.
* `ssh-keygen`: A utility for generating cryptographic key pairs.
* `ssh-copy-id`: A utility that simplifies the process of copying a public key to a remote server.

***

## Methodology

The server hardening process was executed in a series of logical steps, with each command documented below for a detailed record of the actions taken.

### 1. Configure SSH Authentication

First, a more secure authentication method was implemented by generating an SSH key pair on the client machine and copying the public key to the server.

* **Generate an SSH Key Pair:**
    ```bash
    ssh-keygen -t rsa -b 4096
    ```
* **Copy the Public Key to the Server:**
    ```bash
    ssh-copy-id -i /home/kali/Desktop/keyy.pub kali@192.168.157.131
    ```
* **Disable Password Authentication and Root Login:** The SSH configuration file was edited to force all connections to use the new key.
    ```bash
    sudo nano /etc/ssh/sshd_config
    ```
    (Inside the file, `PasswordAuthentication` and `PermitRootLogin` were set to `no`.)
* **Restart the SSH Service:**
    ```bash
    sudo systemctl restart ssh
    ```

### 2. Configure and Enable UFW

Next, a firewall was installed and configured to control network traffic and block unused ports.

* **Install UFW:**
    ```bash
    sudo apt update
    sudo apt install ufw
    ```
* **Set Default Policies:**
    ```bash
    sudo ufw default deny incoming
    sudo ufw default allow outgoing
    ```
* **Allow SSH Traffic:**
    ```bash
    sudo ufw allow ssh
    ```
* **Enable the Firewall:**
    ```bash
    sudo ufw enable
    ```

***

## Findings

The project successfully transformed a default, insecure server into a hardened one. The key findings include:

* **Brute-Force Attack Mitigation:** By disabling password authentication, the server is no longer vulnerable to brute-force attacks on user accounts.
* **Reduced Attack Surface:** The UFW firewall now blocks all incoming connections by default, except for the necessary SSH service. This prevents attackers from probing and exploiting services on other ports.
* **Enhanced Security Posture:** The combination of key-based authentication and a robust firewall significantly enhances the server's overall security, making it more resilient to common cyber threats.

***

## Conclusion & Recommendations

The completion of this task highlights the fundamental importance of **proactive server hardening**. Moving away from default settings is the first and most critical step in securing any system. I recommend the following for continued security:

* **Regular Patching:** Keep all software and the operating system up to date to patch known vulnerabilities.
* **Intrusion Detection:** Implement tools like **Fail2ban** to automatically block malicious IP addresses.
* **Logging and Monitoring:** Set up centralized logging and monitoring to detect and respond to suspicious activity in real-time.

***

## Deliverables

* `README.md`: This report detailing the project overview, methodology, and findings.
* **Screenshots:** Visual evidence of the executed commands and configurations.

---

## Screenshots For POC: 📸

<img width="1919" height="1079" alt="Screenshot 2025-09-16 160450" src="https://github.com/user-attachments/assets/269ef983-3916-4732-84ce-9ef6c4be047c" />


---

<img width="1919" height="1078" alt="Screenshot 2025-09-16 162516" src="https://github.com/user-attachments/assets/c393a1b4-af03-45c2-a6a7-09af16edd27c" />

---

<img width="1467" height="296" alt="Screenshot 2025-09-16 162659" src="https://github.com/user-attachments/assets/96ec8bab-961a-44dc-8e77-4e1622d2fd8f" />

---

<img width="1919" height="1079" alt="Screenshot 2025-09-16 164516" src="https://github.com/user-attachments/assets/5baef2fe-cd97-481a-b660-f413f6af315e" />

