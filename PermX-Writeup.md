### Hack The Box - PermX Walkthrough

#### Step 1: Initial Scanning
- **Target IP:** 10.10.11.198
- **Run an Nmap scan to discover open ports:**
  ```bash
  nmap -sC -sV -oN permx_nmap 10.10.11.198
  ```
- **Results show:**
  - **Port 22 (SSH):** Open.
  - **Port 80 (HTTP):** Website running on Apache.

#### Step 2: Exploring the Website
- **Visit the website on Port 80:**
  - The website is a login page for a web application.
- **Use Gobuster to find hidden directories:**
  ```bash
  gobuster dir -u http://10.10.11.198 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
  ```
- **Find the `/uploads` directory.**

#### Step 3: Exploiting File Upload
- **Check the file upload functionality:**
  - Attempt to upload different file types.
- **Upload a PHP reverse shell disguised as an image file.**

#### Step 4: Getting a Reverse Shell
- **Set up a Netcat listener:**
  ```bash
  nc -lvnp 4444
  ```
- **Access the uploaded file to trigger the reverse shell.**
- **Catch the reverse shell connection.**

#### Step 5: Privilege Escalation
- **Look for privilege escalation opportunities:**
  - Check for running processes or misconfigured files.
- **Find a service or file with elevated privileges.**
- **Exploit to gain root access.**

#### Step 6: Capture the Flags
- **User Flag:** Located in the user’s home directory.
- **Root Flag:** Located in the root directory.
