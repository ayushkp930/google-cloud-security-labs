# Identify Vulnerabilities and Remediation Techniques (XSS Lab)

## Overview

This lab demonstrates how to identify and remediate a common OWASP web application vulnerability: **Cross-Site Scripting (XSS)** using Google Cloud Web Security Scanner.

A vulnerable banking application was deployed on a Compute Engine virtual machine and scanned using Google Cloud's Web Security Scanner to detect XSS vulnerabilities.

---

## Objective

- Deploy a vulnerable web application
- Perform vulnerability scanning
- Identify XSS vulnerabilities
- Implement remediation techniques
- Re-scan to verify security improvements

---

## Technologies Used

- Google Cloud Platform (GCP)
- Compute Engine
- Cloud Shell
- Web Security Scanner
- Python Flask
- OWASP Top 10

---

## Architecture

1. Create static external IP
2. Deploy Compute Engine VM
3. Deploy vulnerable Flask application
4. Configure firewall rules
5. Run Web Security Scanner
6. Identify XSS vulnerability
7. Apply remediation
8. Re-run security scan

---

## Deployment Steps

### 1 Create Static IP


gcloud compute addresses create xss-test-ip-address --region=us-west1


---

### 2 Create Virtual Machine


gcloud compute instances create xss-test-vm-instance
--address=xss-test-ip-address
--no-service-account
--no-scopes
--machine-type=e2-micro
--zone=us-west1-c


---

### 3 Deploy Vulnerable Application


gsutil cp gs://cloud-training/GCPSEC-ScannerAppEngine/flask_code.tar .
tar xvf flask_code.tar
python3 app.py


Application runs on:


http://VM_EXTERNAL_IP:8080


---

## Demonstrating the Vulnerability

The application accepts user input without proper sanitization.

Example payload:

<script>alert('XSS')</script>

Result: Browser executes injected JavaScript.

---

## Vulnerability Scan

Using **Google Cloud Web Security Scanner**:

- Created scan configuration
- Target URL added
- Scanner crawled application
- XSS vulnerability detected

---

## Vulnerability Detected

OWASP Category:


A03: Cross-Site Scripting (XSS)


Cause:


User input was not properly sanitized before rendering in HTML.


---

## Remediation Technique

The vulnerability was fixed by escaping user input before rendering.

Example secure code:


output_string = "".join([html_escape_table.get(c, c) for c in input_string])


This prevents malicious scripts from executing.

---

## Security Best Practices

- Always sanitize user input
- Use output encoding
- Apply Content Security Policy (CSP)
- Use automated security scanning
- Follow OWASP secure coding guidelines

---

## Screenshots

### GCP Project Dashboard
![dashboard](screenshots/01-gcp-console-project.png)

### VM Instance Deployment
![vm](screenshots/02-vm-instance-created.png)

### Cloud Shell Commands
![shell](screenshots/03-cloud-shell-commands.png)

### Vulnerable Application Running
![app](screenshots/05-vulnerable-app-running.png)

### XSS Injection Demonstration
![xss](screenshots/06-xss-injection-demo.png)

### Web Security Scanner Setup
![scanner](screenshots/08-create-scan-config.png)

### Vulnerability Detected
![vuln](screenshots/10-xss-vulnerability-detected.png)

### Code Remediation
![fix](screenshots/11-code-remediation.png)

---

## Key Learning Outcomes

- Deploy vulnerable applications in cloud environments
- Identify web vulnerabilities using automated scanners
- Understand OWASP Top 10 vulnerabilities
- Apply secure coding practices
- Implement vulnerability remediation techniques

---

## Author

Ayush  
Cybersecurity & Cloud Security Enthusiast