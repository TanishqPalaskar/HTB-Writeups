### Hack The Box - Boardlight Walkthrough

#### Step 1: Initial Scanning
- **Target IP:** 10.10.11.186
- **Run an Nmap scan to discover open ports:**
  ```bash
  nmap -sC -sV -oN boardlight_nmap 10.10.11.186
  ```
- **Results show:**
  - **Port 22 (SSH):** Open.
  - **Port 80 (HTTP):** Website running on Apache.

#### Step 2: Exploring the Website
- **Visit the website on Port 80:**
  - The site has a login page.
- **Use Gobuster to find hidden directories:**
  ```bash
  gobuster dir -u http://10.10.11.186 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
  ```
- **Find `/admin` directory.**

#### Step 3: Exploiting the Admin Login
- **Discover the login form in `/admin`.**
- **Use SQL injection to bypass the login:**
  ```sql
  ' OR '1'='1
  ```
- **Gain access to the admin panel.**

#### Step 4: Uploading a Malicious File
- **Find the file upload feature in the admin panel.**
- **Upload a PHP reverse shell disguised as an image file.**

#### Step 5: Gaining Access
- **Set up a listener using Netcat:**
  ```bash
  nc -lvnp 4444
  ```
- **Trigger the reverse shell by accessing the uploaded file.**
- **Catch the shell connection.**

#### Step 6: Privilege Escalation
- **Check the system for privilege escalation opportunities:**
  - Look for misconfigurations or files with elevated permissions.
- **Find and exploit a vulnerable service or file.**

#### Step 7: Capture the Flags
- **User Flag:** Located in the user’s home directory.
- **Root Flag:** Located in the root directory.
