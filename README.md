# EX 5: Metasploit-for-reconnaissance
## Metasploit
Metasploit for reconnaissance in pentesting

## AIM:

To get introduced to Metasploit Framework and to  perform reconnaissance  in pentesting .

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

### EXECUTION STEPS AND ITS OUTPUT:
Find out the ip address of the attackers system
#### OUTPUT:
![ifconfig](https://github.com/Sanjay-2610/Metasploit-for-reconnaissance/assets/91368803/98abda89-3e1d-4095-8737-3dafe2bbcb4e)


Invoke msfconsole:

![msfconsole](https://github.com/Sanjay-2610/Metasploit-for-reconnaissance/assets/91368803/2bfa2cc3-be5d-42de-92b9-4be09dc1f5ba)


Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.

![?](https://github.com/Sanjay-2610/Metasploit-for-reconnaissance/assets/91368803/eef7365f-c25c-4782-acf8-545e5a5950a8)



#### Port Scanning:
Following command is executed for scanning the systems on our local area network with a TCP scan (-sT) looking for open ports between 1 and 1000 (-p1-1000).
msf >  nmap -sT 192.168.1810/24 -p1-1000
#### OUTPUT:
![msf_nmap](https://github.com/Sanjay-2610/Metasploit-for-reconnaissance/assets/91368803/79c1ab87-a4d4-45af-9608-100f63982956)

step4:
use the db-nmap command to scan and save the results into Metasploit's postgresql attached database. In that way, you can use those results in the exploitation stage later.

scan the targets with the command db_nmap as follows.
msf > db_nmap 192.168.181.0/24
#### OUTPUT:

![db_nmap](https://github.com/Sanjay-2610/Metasploit-for-reconnaissance/assets/91368803/b9f09946-463a-40aa-94cd-16fa3a7e1517)


Metasploit has a multitude of scanning modules built in. If we open another terminal, we can navigate to Metasploit's auxiliary modules and list all the scanner modules.
cd /usr/share /metasploit-framework/modules/auxiliary
kali > ls -l
![ll](https://github.com/Sanjay-2610/Metasploit-for-reconnaissance/assets/91368803/dd385bed-ff75-4072-8c18-55d230a6424c)

Search is a powerful command in Metasploit that you can use to find what you want to locate. 
msf >search name:Microsoft type:exploit

The info command provides information regarding a module or platform,
#### OUTPUT
![search](https://github.com/Sanjay-2610/Metasploit-for-reconnaissance/assets/91368803/946a3b99-61b8-414f-a4db-4d0362423923)


Before beginning, set up the Metasploit database by starting the PostgreSQL server and initialize msfconsole database as follows:
systemctl start postgresql
msfdb init
#### MYSQL ENUMERATION
Find the IP address of the Metasploitable machine first. Then, use the db_nmap command in msfconsole with Nmap flags to scan the MySQL database at 3306 port.
db_nmap -sV -sC -p 3306 <metasploitable_ip_address>

![db_nmap](https://github.com/Sanjay-2610/Metasploit-for-reconnaissance/assets/91368803/cb7541cf-31b6-4856-a2b8-74b4769294a4)


Use the search option to look for an auxiliary module to scan and enumerate the MySQL database.
search type:auxiliary mysql

![sql_aux_modules](https://github.com/Sanjay-2610/Metasploit-for-reconnaissance/assets/91368803/960e7d6c-df21-4980-8069-3c2fdaa6bf3f)


use the auxiliary/scanner/mysql/mysql_version module by typing the module name or associated number to scan MySQL version details.
use 11 Or: use auxiliary/scanner/mysql/mysql_version

![use__11](https://github.com/Sanjay-2610/Metasploit-for-reconnaissance/assets/91368803/829a6819-0fc8-4669-87cb-1b3b5b69a9c3)


Use the set rhosts command to set the parameter and run the module, as follows:

![rhosts](https://github.com/Sanjay-2610/Metasploit-for-reconnaissance/assets/91368803/b885a056-2cf4-46cf-8167-e5ed8f01010e)



After scanning, you can also brute force MySQL root account via Metasploit's auxiliary(scanner/mysql/mysql_login) module.

![277977441-5ff81cd2-b37b-4a7e-86c9-4d2a31d262f4](https://github.com/Sanjay-2610/Metasploit-for-reconnaissance/assets/91368803/bc4a5780-8551-40e1-9c2c-1f512f96148e)


set the PASS_FILE parameter to the wordlist path available inside /usr/share/wordlists:
set PASS_FILE /usr/share/wordlistss/rockyou.txt
Then, specify the IP address of the target machine with the RHOSTS command.
set RHOSTS <metasploitable-ip-address>
Set BLANK_PASSWORDS to true in case there is no password set for the root account.
set BLANK_PASSWORDS true

![image](https://github.com/Sanjay-2610/Metasploit-for-reconnaissance/assets/91368803/de1f232b-857c-4873-ad01-85b278ddc05f)

![image](https://github.com/Sanjay-2610/Metasploit-for-reconnaissance/assets/91368803/e4c70a39-2f8f-4d7c-99fe-745115003ac8)

#### RESULT:
The Metasploit framework for reconnaissance is  examined successfully.
