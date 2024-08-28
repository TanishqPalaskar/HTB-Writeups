### Hack The Box - Sea Walkthrough

#### Step 1: Initial Scanning
- **Target IP:** 10.10.11.28
- **Run an Nmap scan to discover open ports:**
  ```bash
  nmap -sC -sV -oN sea_nmap 10.10.11.28
  ```
- **Results show:**
  - **Port 22 (SSH):** Open.
  - **Port 80 (HTTP):** Website running on Apache.

#### Step 2: Exploring the Website
- **Visit the website on Port 80:**
  - The site has a login page.
- **Use Gobuster to find hidden directories:**
  ```bash
  gobuster dir -u http://10.10.11.28 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
  ```
- **Find `/admin` directory.**

#### Step 3: Exploiting the Admin Login
- **Discover the admin login page in `/admin`.**
- **Use SQL injection or brute force to bypass the login.**

#### Step 4: Getting a Reverse Shell
- **Find file upload functionality or other exploit paths.**
- **Upload a PHP reverse shell disguised as another file type.**

#### Step 5: Privilege Escalation
- **Look for privilege escalation opportunities:**
  - Examine services, files, and configurations.
- **Exploit these to gain root access.**

#### Step 6: Capture the Flags
- **User Flag:** Found in the user’s home directory.
- **Root Flag:** Found in the root directory.
