# Forensic Questions

# Forensic Question 1:

  * Forensic Question 1 asks the user to find a hidden message within a file located on their desktop. This question helps to teach components of files, and commands to retrieve the hidden information.

  * To find the hidden message, we need to think about ways data can be hidden in files. One such instance is by using getfattr to find the extended attributes of a file. If you run the sudo getfattr -d <file> command, you will find that the hidden message is:
  <details>
    <summary>Answer:</summary>
<p> "Yahaha! you found me!" </p>
</details>
  

# Forensic Question 2:
   * Forensic Question 2 asks the user to find the path of a hidden backdoor. This backdoor was not actually configured on a port ( i know, i am a fake cybersecurity fan ). For this one, i wanted the user to practice finding weird files.
  <details>
    <summary>Answer:</summary>
<p> /etc/network/connections </p>
</details>

# Forensic Question 3:
   * Forensic Question 3 asks the user to audit the system. Just google the commands, and research them. It's important to not just copy an answer key.
    <details>
    <summary>Answer:</summary>
<p> e85772dc-215f-4db7-b697-23c141c506d4 + 155 </p>
</details>

# Removed unauthorized user:
   * Look through any user account source (terminal command, the user files, or user interface)
  <details>
    <summary>Answer:</summary>
<p> ganon </p>
</details>

# System account has a nologin or false shell:
   * All system accounts need a /bin/false or /usr/sbin/nologin shell (users can't and shouldn't be using these accounts. Check /etc/passwd.
  <details>
    <summary>Answer:</summary>
<p> mail </p>
</details>

# User is not allowed to view the kernel syslog:
   * User's should not have access to groups on the system outside of those strictly approved.
 <details>
    <summary>Answer:</summary>
<p> riju </p>
</details>

# Hidden user removed:
   * This user will not show up in the interface, so where can we find the account?
<details>
    <summary>Answer:</summary>
<p> hackerrr </p>
</details>

# User Urbosa is a member of champions group:
   * This one was in the readme, the command is: sudo addgroup urbosa champions

# Password credit complexity checks added:
   * Check out the /etc/security/pwquality.conf file.

# Password username check enabled:
   * same file as before ^^^

# Extra GECOS strength password checks enabled:
   * set this in the pam config

# Account lockout policy configured:
   * If you know what to add to common-auth, go for it, but i prefer to do it this way.
    
1.) Create the first file using: sudo touch /usr/share/pam-configs/faillock

2.) Edit the file using: sudo nano /usr/share/pam-configs/faillock

3.) Copy and paste (indents have to be there, for the last two values): 

Name: Enforce failed login attempt counter                                                                                                            
Default: no
Priority: 0
Auth-Type: Primary
Auth:
  [default=die] pam_faillock.so authfail
  sufficient pam_faillock.so authsucc

4.) Create the second file using: sudo touch /usr/share/pam-configs/faillock_notify

5.) Edit the file using: sudo nano /usr/share/pam-configs/faillock_notify

6.) Copy and paste: 

Name: Notify on failed login attempts
Default: no
Priority: 1024
Auth-Type: Primary
Auth:
  requisite pam_faillock.so preauth

7.) run sudo pam-auth-update and check notify on failed login attempts and enforce failed login attempt counter.

# ICMP redirects are ignored:
   * the next two configs are in the /etc/sysctl.conf file
   * add this value: net.ipv4.conf.all.accept_redirects = 0

# IPv4 TIME-WAIT ASSASSINATION protection enabled:
   * add this line to the same file:
   * net\.ipv4\.tcp_rfc1337 = 1

# X Server does not allow TCP connections:

# Guest account is disabled:

# Auditd logs local events:

# GRUB signature checks enabled:

# Kernel ExecShield enabled:

# Sudo does not allow core dumps:

# Environment variable defining preloaded libraries is not kept when elevating privileges with sudo:

# Sudo requires authentication:

# Ptrace scope restricted to child processes:

# New kernels cannot be loaded alongside the current one:

# Uncomplicated Firewall (UFW) protection is enabled:

# File is not world-writable:

# User Daruk has an SSH key configured:

# Removed Kali sources from APT repository list:

# Service AppArmor is running:

# Service Rsyslog is running:

# Service Squid is not running:

# Removed plaintext file containing sensitive information:

# Netcat backdoor removed:

# make is not a SUID binary:

# Audit software auditd has been installed:

# Prohibited software wireshark has been removed:

# Prohibited software ettercap has been removed:

# Prohibited software yersinia has been removed:

# The server automatically checks for updates:

# Password authentication disabled in SSH:

# SSH does not process client environment variables:

# SSH does not allow X11 connections:

# SSH key-based authentication is enabled:

# Apache response header set to prod:

# Apache trace requests disabled:

# Anonymous TLS/SSL has been disabled:

# FTP anonymous write commands are disabled:

# FTP PASV security checks enabled:

# FTP does not allow unnecessary client connections
