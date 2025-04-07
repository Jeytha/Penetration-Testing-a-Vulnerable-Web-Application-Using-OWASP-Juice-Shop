# Penetration-Testing-a-Vulnerable-Web-Application-Using-OWASP-Juice-Shop
The project involved setting up and testing the OWASP Juice Shop on Kali Linux using Docker, performing vulnerability scanning, and confirming open ports using Nmap.

Step 1: Install Docker on your Kali Linux machine

             sudo apt-get update
             sudo apt-get install docker.io
             sudo docker pull bkimminich/juice-shop

Step 2: Pull the OWASP Juice Shop Docker image: 

        sudo lsof -i :3000
            
Output:
            COMMAND    PID USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
            docker-pr 4919 root    4u  IPv4  47694      0t0  TCP *:3000 (LISTEN)
            docker-pr 4924 root    4u  IPv6  47701      0t0  TCP *:3000 (LISTEN)

Step 3:  Get Information about the container
         
         sudo docker ps

Output:  CONTAINER ID   IMAGE                   COMMAND                  CREATED                  
STATUS              PORTS                                       NAMES
655d6fb4dd2b   bkimminich/juice-shop   "/nodejs/bin/node /j…"   About a minute  ago   Up About a minute   0.0.0.0:3000->3000/tcp, :::3000->3000/tcp       reverent_cartwright

Step 4:  Access the OWASP Juice Shop web application by navigating to
         
         http://localhost:3000 in your web browser.              

Step 5: Find the correct IP address of the running container:

        sudo docker inspect reverent_cartwright | grep "IPAddress"

Output: "SecondaryIPAddresses": null,
             "IPAddress": "172.17.0.2",
              "IPAddress": "172.17.0.2"

Step 6: Scan for open ports on the machine running OWASP Juice Shop. Perform the scan without Nmap attempting a ping, use the -Pn flag correctly before the target IP. 
        Replace 172.17.0.2 with your own IP.

        nmap -Pn 172.17.0.2

Output: Starting Nmap 7.80 ( https://nmap.org ) at 2025-04-07 13:49 EDT
             Nmap scan report for 172.17.0.2
             Host is up (0.00010s latency).
             Not shown: 999 closed ports
             PORT     STATE SERVICE
             3000/tcp open  ppp
             Nmap done: 1 IP address (1 host up) scanned in 0.19 seconds

Conclusion: The Nmap scan shows that port 3000 is open on the container, which is the port that OWASP Juice Shop is running on.

Now, you should be able to access the Juice Shop application by navigating to 

     http://172.17.0.2:3000 in your web browser. 

