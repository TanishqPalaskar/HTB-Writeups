### Hack The Box - Resource Walkthrough

#### Step 1: Initial Scanning
- **Target IP:** 10.10.11.165
- **Run an Nmap scan to discover open ports:**
  ```bash
  nmap -sC -sV -oN resource_nmap 10.10.11.165
  ```
- **Results show:**
  - **Port 22 (SSH):** Open.
  - **Port 80 (HTTP):** Website running on Apache.

#### Step 2: Exploring the Website
- **Visit the website on Port 80:**
  - The site looks like a resource management application.
- **Use Gobuster to find hidden directories:**
  ```bash
  gobuster dir -u http://10.10.11.165 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
  ```
- **Find the `/admin` directory.**

#### Step 3: Bypassing Admin Login
- **Explore the login page in `/admin`:**
  - Try default credentials or common SQL injection techniques.
- **Use SQL injection to bypass the login:**
  ```sql
  ' OR '1'='1
  ```
- **Gain access to the admin panel.**

#### Step 4: Exploring Admin Features
- **Look for features like file uploads or command execution in the admin panel:**
  - Find an option to upload files.
- **Upload a PHP reverse shell disguised as an image file.**

#### Step 5: Getting a Reverse Shell
- **Set up a Netcat listener to catch the reverse shell:**
  ```bash
  nc -lvnp 4444
  ```
- **Access the uploaded file to trigger the reverse shell:**
  - Navigate to the URL of the uploaded file to execute it.
- **Catch the reverse shell connection.**

#### Step 6: Privilege Escalation
- **Enumerate the system for privilege escalation opportunities:**
  - Look for writable files or services running with elevated privileges.
- **Find a misconfigured service or file with higher permissions.**
- **Exploit it to gain root access.**

#### Step 7: Capture the Flags
- **User Flag:** Found in the user’s home directory.
- **Root Flag:** Found in the root directory.
