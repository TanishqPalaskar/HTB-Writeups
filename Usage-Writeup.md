### Hack The Box - Usage Walkthrough

#### Step 1: Initial Scanning
- **Target IP:** 10.10.11.172
- **Run an Nmap scan to discover open ports:**
  ```bash
  nmap -sC -sV -oN usage_nmap 10.10.11.172
  ```
- **Results show:**
  - **Port 22 (SSH):** Open.
  - **Port 80 (HTTP):** Website running on Apache.

#### Step 2: Exploring the Website
- **Visit the website on Port 80:**
  - The website appears to be a management system.
- **Use Gobuster to find hidden directories:**
  ```bash
  gobuster dir -u http://10.10.11.172 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
  ```
- **Find `/admin` directory.**

#### Step 3: Exploiting Admin Features
- **Find an admin login page in `/admin`.**
- **Use common vulnerabilities or brute force to gain access.**

#### Step 4: Getting a Reverse Shell
- **Explore file upload or command execution features.**
- **Upload a reverse shell or exploit the system to get access.**

#### Step 5: Privilege Escalation
- **Enumerate the system for privilege escalation opportunities:**
  - Look for services running with elevated privileges.
- **Exploit these to gain root access.**

#### Step 6: Capture the Flags
- **User Flag:** Located in the user’s home directory.
- **Root Flag:** Located in the root directory.
