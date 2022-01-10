# Red-Team-vs-Blue-Team
## UGOCHUKWU MMONU

### 01/04/2022

**Overview**

For this project, I was tasked to act as an offensive security, Red Team Member, to exploit a vulnerable Capstone VM. I was also tasked to use Kibana to analyze activity logs taken during the Red Team attack. I analyzed these logs, and used the data collected to develop ideas for new alerts that can improve my monitoring as a Blue Team member.

**Findings**

## Day 1 
Discover the IP address of the Linux Webserver

<img width="723" alt="Screen Shot 2021-12-07 at 8 47 18 PM" src="https://user-images.githubusercontent.com/56059854/148139007-c060f86b-6038-43f0-9605-2a2f1c22a964.png">

Locate the hidden directory on the web

- The Hidden directory was found by adjusting theURL of the company's Webpage to gain access to the hidden directory. Within the directory was a document giving instructions on how to access the company's webdav server.


![68747470733a2f2f692e706f7374696d672e63632f44776d57726763512f696e2d7468652d7365637265742d666f6c6465722e706e67](https://user-images.githubusercontent.com/56059854/148312723-4826808f-ed45-4dce-a914-923694faf7d0.png)


![68747470733a2f2f692e706f7374696d672e63632f3843366a337a396a2f6c6f67696e2d706167652d666f722d7365637265742d666f6c6465722e706e67](https://user-images.githubusercontent.com/56059854/148312665-5cba713e-f39a-4c7c-a2fe-ea1e3638f1f4.png)


Brute force the password for the hidden directory using the hydra command:
   
- hydra -l ashton -P rockyou.txt -s 80 -f -vV 192.168.1.105 http-get/company_folders/secret_folder/
   

![68747470733a2f2f692e706f7374696d672e63632f4c38374a4e3179632f68797264612d70617373776f72642d627265616b2e706e67](https://user-images.githubusercontent.com/56059854/148314372-7d7eaa4b-6d37-4877-8c92-35921cb08e1d.png)

Break the hashed password with the crack station website

 *Username: ryan*
 *password: linux4u*

**Connect to the server via WEBDAV**

- To connect to the webserver i First opened up a file manager window

<img width="1067" alt="Screen Shot 2021-12-08 at 9 22 58 PM" src="https://user-images.githubusercontent.com/56059854/148317597-a13eb465-887e-4169-87db-45bd4acd2477.png">

upload a PHP reverse shell payload

- I used msfvenom to create the payload

<img width="1027" alt="Screen Shot 2021-12-08 at 9 32 01 PM" src="https://user-images.githubusercontent.com/56059854/148317824-6e59d14b-2c2d-4f70-962d-00cd1edcb142.png">


a standard multi/handler exploit was used set up the payload. i was able to drag and drop the PHP payload file into the WebDav folder. the Meterpreter session was opened by clicking on the PHP file. 

<img width="880" alt="Screen Shot 2021-12-08 at 9 34 32 PM" src="https://user-images.githubusercontent.com/56059854/148319265-2acb2293-83b1-4d3c-8954-ec8603098046.png">

METERPRETER SESSION

<img width="1147" alt="Screen Shot 2021-12-08 at 10 36 17 PM" src="https://user-images.githubusercontent.com/56059854/148319377-1477e6a6-3b94-4b20-9020-0eb5aaa9d12e.png">


Capture the flag
- After gaining access to the target's system, i was able to recover the flag in flag.txt


<img width="807" alt="Screen Shot 2021-12-08 at 10 38 47 PM" src="https://user-images.githubusercontent.com/56059854/148322187-0879efc1-b07e-4af7-845d-3e264459034f.png">



## Day 2

**Identify the offensive traffic**

Identify the traffic between you machine and the web machine

- When did the interaction occur?

<img width="829" alt="Screen Shot 2022-01-10 at 4 23 08 PM" src="https://user-images.githubusercontent.com/56059854/148848512-b305a08c-fb75-4d8b-97d4-046bc016af24.png">


- What responses did the victim send back?

<img width="825" alt="Screen Shot 2022-01-10 at 4 23 54 PM" src="https://user-images.githubusercontent.com/56059854/148848594-846f57bb-5088-46e0-8910-1a593ae4ce44.png">


- What data is concerning from the blue team perspective?

 The large amount of error codes looks very concerning, this is evidence of attack attempts on th network. This indicates a sign of bruteforce attack
 
 
Find the request for the hidden directory. In your attack, you found a secret folder. Lets look at that interaction between these two machines.
 
- How many requests were made to this directory? At what time and from which IP address(es)?


- <img width="822" alt="Screen Shot 2022-01-10 at 4 13 19 PM" src="https://user-images.githubusercontent.com/56059854/148847365-3f9f3dc9-ae3c-44d0-8a86-03af20b45523.png">







