FIRST OF ALL I USED NETDISCOVER TOOL TO FIND THE  IP ADDRESS OF CYBER SPOLOIT MACHINE WHICH IS RUNNING IN MY VIRTUAL NETWORK, FROM THIS OUTPUT I IDENTIFIED 192.168.21.139 AS THE LIKELY TARGET IP

<img width="682" height="190" alt="2result of netdiscover" src="https://github.com/user-attachments/assets/abb0df7c-e678-432c-8081-d1e5eb574a36" />

  IP            At MAC Address     Count     Len  MAC Vendor / Hostname      
 -----------------------------------------------------------------------------
 192.168.21.208  36:89:1c:6c:9d:00      3     180  Unknown vendor                                                                                                                                                                         
 192.168.21.115  28:c5:d2:56:25:39      1      60  Intel Corporate                                                                                                                                                                        
 192.168.21.139  08:00:27:0a:c4:8e      1      60  PCS Systemtechnik GmbH   



I THEN PERFORMED AN NMAP SCAN TO ENUMERATE OPEN PORTS AND IDENTIFY RUNNING SERVICES AND OPEN PORTS ON THE TARGET IP
                                                                                                                                                              
 
nmap -sV -sC 192.168.21.139 -Pn


Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-06-24 12:30 EDT
Nmap scan report for 192.168.21.139
Host is up (0.00038s latency).
Not shown: 998 closed tcp ports (conn-refused)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 5.9p1 Debian 5ubuntu1.10 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   1024 01:1b:c8:fe:18:71:28:60:84:6a:9f:30:35:11:66:3d (DSA)
|   2048 d9:53:14:a3:7f:99:51:40:3f:49:ef:ef:7f:8b:35:de (RSA)
|_  256 ef:43:5b:d0:c0:eb:ee:3e:76:61:5c:6d:ce:15:fe:7e (ECDSA)
80/tcp open  http    Apache httpd 2.2.22 ((Ubuntu))
|_http-server-header: Apache/2.2.22 (Ubuntu)
|_http-title: Hello Pentester!
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 6.74 seconds

SINCE HTTP AND SSH PORT WERE OPEN, I FIRST OPENED THE TARGET IP IN MY BROWSER

<img width="1916" height="872" alt="3 browsing ip" src="https://github.com/user-attachments/assets/ecc26615-b2c0-4914-aa33-607a8c5dda41" />

THE SITE SHOWED A SIMPLE MESSAGE "HELLO PENTESTER" I THEN CHECKED THE SOURCE PAGE,THERE I FOUND A USERNAME : itsskv

<img width="562" height="111" alt="4 source code found a user name" src="https://github.com/user-attachments/assets/b304ac3e-1b5a-4196-97e6-f99606dbc40e" />


THERE WAS NO PASSWORD SHOWN ON THE PAGE

NEXT I RAN DIRB TO LOOK FOR HIDDEN FOLDER OR FILES

I FOUND SOME DIRECTORIES BUT ONE FILE WAS VERY INTRESTING ,"ROBOTS.TXT"

<img width="766" height="201" alt="5found a hash file" src="https://github.com/user-attachments/assets/b84293bd-55bd-4fd4-afc1-f046b544e97c" />


I GUESS I FOUND A PASSWORD HASH                                                

R29vZCBXb3JrICEKRmxhZzE6IGN5YmVyc3Bsb2l0e3lvdXR1YmUuY29tL2MvY3liZXJzcGxvaXR9 

I DIDNT KNOW WHAT TYPE OF HASH THIS WAS SO I USED A WEBSITE CALLED DCODE.FR
ON DCODE I SEARCHED FOR A TOOL NAMED HASH IDENTIFIER 

<img width="1848" height="518" alt="6 used dcode hash identifier" src="https://github.com/user-attachments/assets/ca7134be-e16a-490d-9a73-030dcc7f63bc" />


BASE64 ENCODED

THEN I USED DCODE'S BASE64 DECODER

GOT THE FIRST FLAG AND POSSIBLY SSH PASSWORD,

<img width="838" height="195" alt="7 decrypted hash" src="https://github.com/user-attachments/assets/af4b8159-afcb-4d17-91f4-d6dbedee68c9" />


Flag1: cybersploit{youtube.com/c/cybersploit}


LETS TRY LOGGING INTO SSH USING USERNAME : itsskv , PASSWORD: cybersploit{youtube.com/c/cybersploit}

<img width="662" height="308" alt="8 we got logged in" src="https://github.com/user-attachments/assets/5ac401c6-05dd-4d20-9b2e-f4976d8ae844" />


SUCCESFULLY LOGGED INTO ITSSKV !!!!!

 USED LS COMMAND AND FOUND FLAG2.TXT
 
<img width="1920" height="192" alt="9 got a binary in flag 2" src="https://github.com/user-attachments/assets/827bb7c7-5858-4778-9a4f-7627538d08ad" />

USED CAT FLAG2.TXT


01100111 01101111 01101111 01100100 00100000 01110111 01101111 01110010 01101011 00100000 00100001 00001010 01100110 01101100 01100001 01100111 00110010 00111010 00100000 01100011 01111001 01100010 01100101 01110010 01110011 01110000 01101100 01101111 01101001 01110100 01111011 01101000 01110100 01110100 01110000 01110011 00111010 01110100 00101110 01101101 01100101 00101111 01100011 01111001 01100010 01100101 01110010 01110011 01110000 01101100 01101111 01101001 01110100 00110001 01111101



USED A WEBSITE NAME CRYPTI FOR DECODING,DECODED BINARY:
flag2: cybersploit{https:t.me/cybersploit1}



I  STILL DOSENT HAVE ROOT PRIVILEAGE SO I USED UNAME -A COMMAND TO FIND THE VERSION OF KERNEL 

<img width="963" height="42" alt="10 version" src="https://github.com/user-attachments/assets/9246305d-ff7b-44a2-8aea-938f4a5901cb" />

 3.13.0-32-generic

WE FOUND THE KERNEL VERSION


BROWSED KERNAL VERSION,THERE WAS A LOCAL PRIVILEAGE ESCALATION EXPLOIT AVAILABLE


CVE:
2015-1328
<img width="1842" height="482" alt="11 found kernal exploit" src="https://github.com/user-attachments/assets/016ffbe1-625e-414a-9151-ffb9386ecabc" />


LETS COPY THIS AND PASTE IN TMP FOLDER 

NAMED IT EXPLOIT.C  


USED GCC EXPLOIT.C -o EXPLOIT

<img width="988" height="236" alt="13 escalated privileage" src="https://github.com/user-attachments/assets/e216ff55-f810-468e-8ee9-a5f6227f3ce8" />


./EXPLOIT

ROOT SHELL OPENED


WE MOVED ON TO ROOT FOLDER AND THERE OUR FINAL FLAG WAS WAITING FOR US







<img width="1828" height="393" alt="14 got final flag" src="https://github.com/user-attachments/assets/b212ad66-3163-4997-bd76-c18d27efeefb" />










 ______ ____    ____ .______    _______ .______          _______..______    __        ______    __  .___________.
 /      |\   \  /   / |   _  \  |   ____||   _  \        /       ||   _  \  |  |      /  __  \  |  | |           |
|  ,----' \   \/   /  |  |_)  | |  |__   |  |_)  |      |   (----`|  |_)  | |  |     |  |  |  | |  | `---|  |----`
|  |       \_    _/   |   _  <  |   __|  |      /        \   \    |   ___/  |  |     |  |  |  | |  |     |  |     
|  `----.    |  |     |  |_)  | |  |____ |  |\  \----.----)   |   |  |      |  `----.|  `--'  | |  |     |  |     
 \______|    |__|     |______/  |_______|| _| `._____|_______/    | _|      |_______| \______/  |__|     |__|     
                                                                                                                  

   _   _   _   _   _   _   _   _   _   _   _   _   _   _   _  
  / \ / \ / \ / \ / \ / \ / \ / \ / \ / \ / \ / \ / \ / \ / \ 
 ( c | o | n | g | r | a | t | u | l | a | t | i | o | n | s )
  \_/ \_/ \_/ \_/ \_/ \_/ \_/ \_/ \_/ \_/ \_/ \_/ \_/ \_/ \_/ 

flag3: cybersploit{Z3X21CW42C4 many many congratulations !}






itsskv





Flag1: cybersploit{youtube.com/c/cybersploit}










good work !
flag2: cybersploit{https:t.me/cybersploit1}






 3.13.0-32-generic
