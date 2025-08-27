# b3dr0ck
<img width="196" height="255" alt="b3drock" src="https://github.com/user-attachments/assets/63203060-0009-4192-954a-c1ef6ddc7572" />

## Server trouble in Bedrock.

![fredAndBarney](https://github.com/user-attachments/assets/1b09c0e0-5f08-4bed-ac5a-40799fd8755b)

Fred Flintstone   &   Barney Rubble!

Barney is setting up the ABC webserver, and trying to use TLS certs to secure connections, but he's having trouble. Here's what we know...

He was able to establish nginx on port 80,  redirecting to a custom TLS webserver on port 4040
There is a TCP socket listening with a simple service to help retrieve TLS credential files (client key & certificate)
There is another TCP (TLS) helper service listening for authorized connections using files obtained from the above service
Can you find all the Easter eggs?

## step 1 : 
I did the port scan using rustscan

<img width="714" height="62" alt="Screenshot From 2025-08-27 15-00-54" src="https://github.com/user-attachments/assets/e683c27a-6651-4c2a-8241-b27fbc612fb0" />

<img width="1100" height="418" alt="Screenshot From 2025-08-27 15-02-20" src="https://github.com/user-attachments/assets/78f7c0de-f935-4717-a40f-1db8eb641ba6" />

I was not enough for me . so, I used nmap --> (This Attack VM was automatically terminated twice. So I deploy it agian)

<img width="962" height="62" alt="Screenshot From 2025-08-27 15-03-02" src="https://github.com/user-attachments/assets/a7bf1a21-929c-4a93-a26b-6ea2ceb70caf" />


https://github.com/user-attachments/assets/93d8114f-b336-4237-b39c-aee034fe157c

1. First question hint is Explore the higher ports, one is ready for a TLS socket with key & cert obtained from port 9009.

port 9009 pichat service is running. **Pichat Server operates on port 9009 and is utilized as part of a peer-to-peer (P2P) chat application suite. It facilitates the real-time exchange of messages directly between clients without relying on centralized infrastructure. Designed primarily for instant communication, its P2P nature offers benefits such as reduced server overhead and potentially enhanced privacy compared to centralized services.**

so, using netcat ,

``` bash
nc 10.10.168.21 9009
```
<img width="904" height="794" alt="Screenshot From 2025-08-27 16-26-12" src="https://github.com/user-attachments/assets/81ab8c41-bfdf-4250-8f8d-53f5623fa650" />
<img width="904" height="818" alt="Screenshot From 2025-08-27 16-26-40" src="https://github.com/user-attachments/assets/dc6b3c4c-fd2c-4adf-8f4d-69d723157b7a" />


**Now Try connecting using:**
``` bash
socat stdio ssl:MACHINE_IP:54321,cert=<CERT_FILE>,key=<KEY_FILE>,verify=0
```
using socat we can connect to the Barney as bellow.

<img width="942" height="730" alt="Screenshot From 2025-08-27 16-34-07" src="https://github.com/user-attachments/assets/30d1c37a-9665-4269-a8d0-82425f25a323" />

This one reveals barney's passwd. so i tryed username as barney and used above password. and i'm in...

<img width="942" height="205" alt="Screenshot From 2025-08-27 16-40-03" src="https://github.com/user-attachments/assets/1d118388-6f17-444d-8b37-19c680464a13" />

## 2. What is fred's password?

<img width="568" height="546" alt="Screenshot From 2025-08-27 16-41-50" src="https://github.com/user-attachments/assets/213c7f52-94b5-4898-a17a-e5e05812ab61" />

<img width="1044" height="134" alt="Screenshot From 2025-08-27 16-42-23" src="https://github.com/user-attachments/assets/c87fb0cf-26aa-4935-9ec0-ab9e11ecb2c2" />

**Barney can run the following command**

<img width="978" height="191" alt="Screenshot From 2025-08-27 16-42-37" src="https://github.com/user-attachments/assets/89bfdb90-6dbc-4820-b29f-678bd6667894" />

<img width="927" height="314" alt="Screenshot From 2025-08-27 16-42-46" src="https://github.com/user-attachments/assets/5adb96cc-77bb-49f0-a092-2106a91ab9b8" />

<img width="956" height="875" alt="Screenshot From 2025-08-27 16-43-26" src="https://github.com/user-attachments/assets/b3809f72-fe57-46c7-a45a-3689ad74689b" />

**save this key and cert for fred**

<img width="948" height="476" alt="Screenshot From 2025-08-27 16-43-54" src="https://github.com/user-attachments/assets/d03a2fdb-481e-423c-855b-4a9a8df5caac" />

## 3. What is the fred.txt flag?

<img width="876" height="164" alt="Screenshot From 2025-08-27 16-55-04" src="https://github.com/user-attachments/assets/45fb26b3-6486-4099-984a-79d1c02b959c" />

## 4. What is the root.txt flag?

**using ```sudo -l``` in user fred**

I used linpeas ;-)

<img width="1041" height="184" alt="Screenshot From 2025-08-27 16-59-42" src="https://github.com/user-attachments/assets/9efeaebe-2a98-4a94-bb27-ef80be0337d2" />


<img width="1066" height="244" alt="Screenshot From 2025-08-27 17-02-09" src="https://github.com/user-attachments/assets/1430507e-aeb4-48cf-af0e-31570219b890" />

**using base64**
<img width="1322" height="88" alt="Screenshot From 2025-08-27 17-02-25" src="https://github.com/user-attachments/assets/7b5106e5-f169-4734-a6c4-2c821537a06d" />


<img width="1910" height="683" alt="Screenshot From 2025-08-27 17-02-46" src="https://github.com/user-attachments/assets/e52aa9e1-550d-4b4f-b237-02cf5be32c71" />

**got the passwd**
<img width="1910" height="683" alt="Screenshot From 2025-08-27 17-02-59" src="https://github.com/user-attachments/assets/26f23fad-69df-4f0a-95f4-08c4f6879acb" />


<img width="753" height="177" alt="Screenshot From 2025-08-27 17-03-27" src="https://github.com/user-attachments/assets/a8401ced-8ad7-4b0b-aa00-c6b357286a64" />



