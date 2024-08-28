### Hack The Box - Blurry Walkthrough

#### Step 1: Initial Scanning
- **Target IP:** 10.10.11.183
- **Run an Nmap scan to discover open ports:**
  ```bash
  nmap -sC -sV -oN blurry_nmap 10.10.11.183
  ```
- **Results show:**
  - **Port 22 (SSH):** Open.
  - **Port 80 (HTTP):** Website running on Apache.

#### Step 2: Exploring the Website
- **Visit the website on Port 80:**
  - Check for anything interesting but nothing stands out immediately.
- **Use Gobuster to find hidden directories:**
  ```bash
  gobuster dir -u http://10.10.11.183 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
  ```
- **Find `/upload` directory.**

#### Step 3: Exploiting the Upload Function
- **Check the upload function on the site:**
  - Try uploading various file types.
- **Discover that image files are accepted.**
- **Use a PHP reverse shell disguised as an image and upload it.**

#### Step 4: Gaining a Reverse Shell
- **Set up a listener using Netcat:**
  ```bash
  nc -lvnp 4444
  ```
- **Execute the uploaded PHP shell to connect back to your listener.**
- **Catch the reverse shell and gain access to the machine.**

#### Step 5: Privilege Escalation
- **Enumerate the system to find ways to increase privileges:**
  - Look at running processes, scheduled tasks, or misconfigurations.
- **Find a vulnerable service or file running as a higher privilege user.**
- **Exploit this to get a higher-level shell.**

#### Step 6: Root Access
- **Gain root access by exploiting the vulnerable service or file.**
- **You now have full control of the machine.**

#### Step 7: Capture the Flags
- **User Flag:** Located in the user's home directory.
- **Root Flag:** Located in the root directory.
