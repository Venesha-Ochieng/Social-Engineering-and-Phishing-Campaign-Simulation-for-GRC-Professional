# INTERNATIONAL CYBERSECURITY AND DIGITAL FORENSICS ACADEMY

## GRC103: Risk Assessment and Management Techniques

### Week 2 Practical Laboratory:
# Social Engineering and Phishing Campaign Simulation for GRC Professional

**Full Name:** Venesha Adhiambo Ochieng  
**Registration Number:** C11/26/CGRCE/17566  
**Email Address:** c11.cgrce2617566@icdfa.edu.ng  
**Cohort / Batch:** Cohort11  
**Date Submitted:** 2nd November 2026

# Social Engineering & Phishing Campaign Simulation for GRC Professionals

## 1. Introduction

GRC analysts, technical vulnerabilities are only one part of the risk landscape. The human element is often the most exploited attack vector. This lab focuses on **social engineering**, specifically phishing, which is the leading cause of data breaches. You will step into the shoes of both an attacker (to understand the mechanics) and a GRC auditor (to measure risk and policy effectiveness). Your goal is not to trick users, but to objectively measure organizational risk and the effectiveness of security awareness controls.

## 2. Scenario

The CISO is concerned about the organization's resilience to phishing attacks. You have been authorized to conduct a **controlled, internal, and benign phishing campaign** against a test group of users (in this case, a simulated environment). The objective is to gather data on the click-through rate, credential submission rate, and overall user susceptibility to inform future training budgets, policy updates, and risk calculations.

## 3. Lab Setup

- **Your Machine:** Kali Linux (Attacker/Auditor) - IP: 192.168.x.x
  - *We will install a new tool on Kali for this lab.*
- **Target (Simulated User Environment):** We will simulate the target users by sending emails to ourselves or a test mailbox. No actual users will be targeted.
- **Phishing Framework:** **GoPhish** (Open-source phishing toolkit).
- **Target Website:** We will clone the login page of a common internal service (e.g., a fake VPN portal hosted on the Kali machine).

# 4. Step-by-Step Instructions

# Phase 1: Setup and Preparation

## Step 1: Install GoPhish

- **Task:** Download and set up the phishing framework.
- **Create a working directory**
![Screenshot 1](1.png)

### Commands:

Download the latest version of GoPhish for Linux (check for the latest version on their website)

```bash
wget https://github.com/gophish/gophish/releases/download/v0.12.1/gophish-v0.12.1-linux-64bit.zip
```
![Screenshot 2](2.png)

Unzip the file

```bash
unzip gophish-v0.12.1-linux-64bit.zip -d gophish/
```
![Screenshot 3](3.png)

Navigate to the directory

```bash
cd gophish/
```
![Screenshot 4](4.png)

Make the binary executable

```bash
chmod +x gophish
```
![Screenshot 5](5.png)

Check configuration server

![Screenshot 6](6.png)

Make changes to phish-server listen url
![Screenshot 7](7.png)

Run GoPhish

```bash
./gophish
```
![Screenshot 8](8.png)

- **Action:** Note the admin interface URL in the terminal (usually `https://127.0.0.1:3333`). Open this in your Firefox browser and accept the SSL warning. Log in with the default credentials (`admin / gophish`).

---
![Screenshot 9](9.png)

## Step 2: Configure Sending Profile

- **Task:** Tell GoPhish how to send emails. For this lab, we will use a local SMTP server or a test service like **Mailtrap.io** (safer and recommended to avoid being flagged as spam).

- **Action (Using Mailtrap - Free Tier):**

1. Go to https://mailtrap.io/ and create a free account.
![Screenshot 10](10.png)

3. In your Mailtrap inbox, find the **SMTP settings** under the "Integrations" tab.
![Screenshot 11](11.png)

5. In GoPhish, go to **Sending Profiles** > **New Profile**.

6. Name: **Mailtrap Test**

7. From: **Security Team <security-test@yourcompany.com>** (Use a convincing alias).

8. Use the Host, Port, Username, and Password provided by Mailtrap.

9. Click **Save Profile**.

---
![Screenshot 12](12.png)

![Screenshot 13](13.png)

## Step 3: Create a Landing Page

- **Task:** Clone a legitimate login page to use as the phishing destination.

- **Action:**

1. In GoPhish, go to **Landing Pages** > **New Page**.
   ![Screenshot 14](14.png)

3. Name: **Fake VPN Portal**

4. HTML: Click **Import Site**. Enter the URL of a common login page you want to clone (e.g., your university's VPN portal, a fake internal wiki, or even a Microsoft O365 login). GoPhish will fetch the HTML.

5. **Critical GRC Step:** Check the box **"Capture Submitted Data"** and **"Capture Passwords"**. This is how we will measure success. Also, check **"Redirect to"** and enter a URL like `https://www.yourcompany.com/security-training` to simulate sending users to a training page after they "log in".

---
![Screenshot 15](15.png)

## Step 4: Create an Email Template

- **Task:** Craft a convincing phishing email.

- **Action:**

1. Go to **Email Templates** > **New Template**.
![Screenshot 16](16.png)
2. Name: **VPN Password Reset Required**

3. Subject: **Action Required: Your VPN Password Expires in 24 Hours**

4. HTML: Click **Import Site** and paste the HTML of a well-crafted professional email. Alternatively, write a simple text:

```html
Dear {{.FirstName}},
<br><br>
Our records indicate that your VPN password must be reset due to a system-wide security update. Failure to do so within 24 hours will result in loss of access.
<br><br>
Please click here to reset your password immediately: {{.URL}}
<br><br>
Thank you,
<br>
IT Security Team
```
![Screenshot 17](17.png)

5. Note the use of `{{.FirstName}}` and `{{.URL}}`. These are GoPhish variables for personalization and the phishing link.

---

## Step 5: Define Your Target Group

- **Task:** Create a group of test users. Since this is a lab, we will use ourselves.

- **Action:**

1. Go to **Users & Groups** > **New Group**.
![Screenshot 18](18.png)
2. Name: **Lab Test Group**

3. Add yourself as a target. Example:

   - Email: `your.test.email@gmail.com` (or a test account)
   - First Name: Lab
   - Last Name: User
   - Position: Employee

> *In a real audit, this would be a CSV import of the test department.*

---
![Screenshot 19](19.png)

---
