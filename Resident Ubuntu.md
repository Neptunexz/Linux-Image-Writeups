# Forensic Question 1
  - From prior knowledge and research you could search in files for files associated with different backdoors.
  - Hint: appctl
 <details>
    <summary>Answer:</summary>
<p> /usr/share/bin/appctl & /etc/systemd/system/.appctl.service </p>
</details>

# Forensic Question 2
  - Whenever a forensic question asks for anything involving system information like this one does, you can usually just use google and find the command

  - For this specific question, you need to use the <> command to find the answer.

  <details>
    <summary>Answer:</summary>
<p> 55 </p>
</details>

# Forensic Question 3  
  - For this forensic, the simple approach is the correct one. If you check out your (leon's) search history, you will find an unusual website.

  - No command required

<details>
    <summary>Answer:</summary>
<p> leon & https://pictureofahotdog.com </p>
</details>

# Removed unauthorized system account
  - For this vulnerability, there are three routes of finding unauthorized users. UI, /home directory, and the /etc/passwd file all show the accounts on the system to varrying degrees. For this one, you need to check out /etc/passwd.

  - Once you locate the user account, you can use the sudo deluser <username> command to rmeove them.

<details>
    <summary>Answer:</summary>
<p> network </p>
</details>

# System account does not have a password set
  - For this vulnerability, you can check out /etc/shadow and check out the accounts with passwords. If the account does not belong to a user account AND has a password set, delete the password from the line in the file.

<details>
    <summary>Answer:</summary>
<p> bin </p>
</details>

# System account has a nologin or false shell
  - For this vulnerablity, you can check out /etc/passwd, where the shell environments are set for all accounts. All system accounts need to have a /bin/false or a /usr/sbin/nologin shell set, instead of /bin/bash.

  <details>
    <summary>Answer:</summary>
<p> tcpdump </p>
</details>

# 'user' is not allowed to view the 'group'
  - For security purposes, users should not be apart of groups they do not need to be in. Check out /etc/group and see what users are in what groups.

  <details>
    <summary>Answer:</summary>
<p> claire cannot view the proxy </p>
</details>

# A secure maximum password age has been set
  - This is standard practice. Just change it to 30-90 days in /etc/login.defs.

# Password encryption method set to SHA512
  - This one is a little less common. Also configurable in /etc/login.defs. SHA512 is the best security practice here.

# A secure number of login retries is configured
  - This one is (also) configured in /etc/login.defs. Anything between 1-5 is acceptable.

# Account lockout policy configured
  - If you know what to add to common-auth, go for it, but i prefer to do it this way.
    
1.) Create the first file using: sudo touch /usr/share/pam-configs/faillock

2.) Edit the file using: sudo nano /usr/share/pam-configs/faillock

3.) Copy and paste (indents have to be there): 
Name: Enforce failed login attempt counter
Default: no
Priority: 0
Auth-Type: Primary
Auth:
  [default=die] pam_faillock.so authfail
  sufficient pam_faillock.so authsucc

4.) Create the second file using: /usr/share/pam-configs/faillock_notify

5.) Edit the file using: sudo nano /usr/share/pam-configs/faillock_notify

6.) Copy and paste: 
Name: Notify on failed login attempts
Default: no
Priority: 1024
Auth-Type: Primary
Auth:
requisite pam_faillock.so preauth

7.) run sudo pam-auth-update and check notify on failed login attempts and enforce failed login attempt counter.

# Send redirects are ignored
  - This is just one of those things you should know to set in ipv4 settings. Keep this file open as several things need to be configured here. The file is /etc/sysctl.conf.

 <details>
    <summary>Answer:</summary>
<p> net.ipv4.conf.all.send_redirects = 0 
    net.ipv4.conf.default.send_redirects = 0
</p>
</details> 

# Martian packet logging is enabled
  - In the same file as ^^
 
 <details>
    <summary>Answer:</summary>
<p> net.ipv4.conf.all.log_martians = 1
</p>
</details> 

# IPv4 TIME_WAIT ASSASSINATION protection enabled
  - In the same file as ^^

 <details>
    <summary>Answer:</summary>
<p> net.ipv4.tcp_rfc1337 = 1
</p>
</details> 

# gdm3 does not allow root login
  - We can configure gdm3 (our display manager) in the /etc/gdm3/custom.conf file. Make sure root login is not allowed (set to false).

# Removed insecure sudoers rule
  - Type in sudo visudo.
  - Two lines need deleted.
 
 <details>
    <summary>Answer:</summary>
<p> Defaults        !env_reset & Defaults        env_keep += "PATH"


</p>
</details> 

# Kernel address space layout randomization (ASLR) is enabled
  - In /etc/sysctl.conf, we can configure this.

 <details>
    <summary>Answer:</summary>
<p> kernel.randomize_va_space = 2
  (1 is also acceptable, 2 is more secure though.)
</p>
</details> 

# Loading TTY line disciplines to the CAP_SYS_MODULE is disabled
  - In the same file as ^^

 <details>
    <summary>Answer:</summary>
<p> dev.tty.ldisc_autoload=0
</p>
</details> 

# New kernels cannot be loaded alongside the current one
  - In the same file as ^^

 <details>
    <summary>Answer:</summary>
<p> kernel.kexec_load_disabled=1
</p>
</details> 

# Sudo developer mode is disabled
  - Some settings for sudo can be configured in the /etc/sudo.conf file, which we will be taking a look at.

  - Sudo developer mode in particular needs to be disabled because we don't need this enabled. (duh)

 <details>
    <summary>Answer:</summary>
<p> Set developer_mode false
</p>
</details> 

# Sudo does not allow core dumps
  - Core dumps leave the system open to increased risks, so we must disable it. Same file as ^^

 <details>
    <summary>Answer:</summary>
<p> Set disable_coredump true
</p>
</details> 

# Sudo does not probe interfaces
  - Probes of all kinds are bad, what can i say

 <details>
    <summary>Answer:</summary>
<p> Set probe_interfaces false
</p>
</details> 

# Uncomplicated Firewall (UFW) protection is enabled
  - This is one of those common sense things
  - Just run sudo systemctl start ufw

# Squid directory is not world-writable
  - just run sudo chmod 640 on the directory

# Removed insecure /etc/hosts entries
  - What looks out of place here?

<details>
    <summary>Answer:</summary>
<p> 127.0.1.1       walmart.com
</p>
</details> 

# Nginx has been disabled or removed
  - sudo systemctl disable/stop nginx

# Service AppArmor is running
  - ^^ same as the last one but with enable/start

# Malicious crontab configuration removed
  - check crontab
  - remove the stuff

# Removed plaintext file containing sensitive information
  - Use file UI and make sure hidden files are enabled. look around and stuff

<details>
    <summary>Answer:</summary>
<p> /etc/.p/.1/evil
</p>
</details> 

# Netcat backdoor removed
  - You could check ports and stuff, but i will level with you, its not running on a port LMAO
  - Hint: its within /etc

<details>
    <summary>Answer:</summary>
<p> /etc/network/network-services/ip-address
</p>
</details> 

# Removed appctl backdoor
  - Theres another one, tied to forensics. i dunno how to help

<details>
    <summary>Answer:</summary>
<p> /etc/network/network-services/ip-address & /etc/systemd/system/appctl.service
</p>
</details> 

# Firefox Checks the current validity of certificates
  - Just know to configure firefox settings :p

# '' is not a SUID binary
  - Run something like chkrootkit or rkhunter to find these SUID binaries.

# Prohibited software has been removed
  - Literally just know softwares and you can delete them
  - Run sudo apt autoremove <program>

  <details>
    <summary>Answer:</summary>
<p> sucrack
</p>
</details> 

# Prohibited software has been removed
  - ^^

<details>
    <summary>Answer:</summary>
<p> john
</p>
</details> 

# Prohibited software has been removed
  - ^^
<details>
    <summary>Answer:</summary>
<p> python3-scapy (scapy)
</p>
</details> 

# Prohibited software has been removed
  - ^^

<details>
    <summary>Answer:</summary>
<p> nmap
</p>
</details> 

# The server automatically Checks for updates
  - Another systemctl command
  - click answer to find service

<details>
    <summary>Answer:</summary>
<p> unattended-upgrades
</p>
</details> 

# Samba encryption is required
  - All samba config is in /etc/samba/smb.conf. You can scout this one out yourself.

# Samba SMB1 protocol disabled
  - Minimum protical needs to NOT be SMB1

# Samba SMB2/3 protocol enabled
  - Make sure protocol is a lot higher

<details>
    <summary>Answer:</summary>
<p> server min protocol = SMB2
</p>
</details> 

# Samba does not allow guest users
  - Guest users are very bad, disable them.

<details>
    <summary>Answer:</summary>
<p> usershare allow guests = yes
</p>
</details> 

# Samba share obeys pam restrictions
  - this basically just means samba will follow pam configs

  <details>
    <summary>Answer:</summary>
<p> obey pam restrictions = yes
</p>
</details> 
     

# Samba uses user-level security
  - User level security i guess i dunno

   <details>
    <summary>Answer:</summary>
<p> security = share
</p>
</details>    

# Samba server signing is mandatory  
  - sevrer signing is just something to configure
  
  <details>
    <summary>Answer:</summary>
<p> server signing = optional
</p>
</details>  

# Squid does not allow HTTP connections
  - All squid config is in /etc/squid/squid.conf
  - HTTPS ONLY!!!!!!!1!1!

  <details>
    <summary>Answer:</summary>
<p> file should not contain: http_access allow all
</p>
</details>  

# Squid port set to 443
  - README tells us to change the port, so change the port 😠
  <details>
    <summary>Answer:</summary>
<p> http_port 3128
</p>
</details>  

# Squid has a localhost manager
  - squid needs a localhost manager, so give it one (use google i dont know)

 <details>
    <summary>Answer:</summary>
<p> deny localhost manager
</p>
</details> 


# Squid proxy is configured for Firefox
  - This is one of those firefox things. Google it tbh or ill walk you thru it wink wink

 <details>
    <summary>Answer:</summary>
<p> 192.175.127.211 & 443 & 1
</p>
</details> 

# Squid denies icp connections
  - icp connections are bad bc icp is two rlly weird creeps

 <details>
    <summary>Answer:</summary>
<p> icp_access allow all
</p>
</details> 

 <details>
    <summary>Answer:</summary>
<p> http_access allow conn_limit
</p>
</details> 
