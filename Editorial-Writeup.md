### Hack The Box - Editorial Walkthrough

#### Step 1: Initial Scanning
- **Target IP:** 10.10.11.211
- **Run an Nmap scan to discover open ports:**
  ```bash
  nmap -sC -sV -oN editorial_nmap 10.10.11.211
  ```
- **Results show:**
  - **Port 22 (SSH):** Open.
  - **Port 80 (HTTP):** Website running on Apache.

#### Step 2: Exploring the Website
- **Visit the website on Port 80:**
  - Notice it is a blog page.
- **Use Gobuster to find hidden directories:**
  ```bash
  gobuster dir -u http://10.10.11.211 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
  ```
- **Find the `/admin` directory.**

#### Step 3: Bypassing Admin Login
- **Discover a login form in the `/admin` directory.**
- **Try common SQL injection payloads to bypass the login:**
  ```sql
  ' OR 1=1 --
  ```
- **Successfully bypass the login using SQL injection.**

#### Step 4: Uploading a Malicious File
- **Explore the admin panel and find an option to upload files.**
- **Upload a PHP reverse shell disguised as an image.**

#### Step 5: Gaining a Reverse Shell
- **Set up a listener using Netcat:**
  ```bash
  nc -lvnp 4444
  ```
- **Trigger the reverse shell by accessing the uploaded file.**
- **Catch the reverse shell connection.**

#### Step 6: Privilege Escalation
- **Enumerate the system to find a way to escalate privileges:**
  - Look for misconfigurations, such as writable files with higher permissions.
- **Find a misconfigured file or service running with elevated privileges.**
- **Exploit this to gain root access.**

#### Step 7: Capture the Flags
- **User Flag:** Found in the user’s home directory.
- **Root Flag:** Found in the root directory.
