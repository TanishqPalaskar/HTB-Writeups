### Hack The Box - Runner Walkthrough

#### Step 1: Initial Scan
- **Target IP:** 10.10.10.209
- **Start by scanning the machine using Nmap:**
  ```bash
  nmap -sC -sV -oN runner_nmap 10.10.10.209
  ```
- **What we found:**
  - **Port 80:** Website running on Apache.

#### Step 2: Exploring the Website
- **Open the website in your browser.**
- **Use Gobuster to find hidden directories:**
  ```bash
  gobuster dir -u http://10.10.10.209 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
  ```
- **Discover the `/src` directory with Python scripts.**
- **Download and review the `backup.py` script.**

#### Step 3: Looking at the Python Script
- **Check out the `backup.py` script:**
  - It's used to back up files on the server.
  - Look for weaknesses in the script.

#### Step 4: Getting Initial Access
- **Exploit a weakness in the script:**
  - The script doesn’t properly check what’s being inputted, which lets us inject harmful code.
- **Create a reverse shell payload and add it to the script.**

#### Step 5: Opening a Reverse Shell
- **Set up a listener to catch the shell using Netcat:**
  ```bash
  nc -lvnp 4444
  ```
- **Run the injected script and catch the reverse shell connection.**

#### Step 6: Moving to Full Control
- **Look around the system for possible ways to become the main user:**
  - You find a backup script that runs automatically with higher privileges.
- **Change the script to open a higher-level shell.**

#### Step 7: Getting Root Access
- **Wait for the system to run the modified script.**
- **Get full control of the system with a root shell.**

#### Step 8: Capture the Flags
- **User Flag:** Found in the user's home directory.
- **Root Flag:** Found in the root directory.
