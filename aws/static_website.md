Steps to Host a Static Website on AWS (with Explanation)

<img width="1024" height="1536" alt="building static webserver" src="https://github.com/user-attachments/assets/8f0ee275-202e-47e7-a14a-d0cf0ca95ff7" />


Step 1: Launch an EC2 Instance

    What you do:
        - Go to AWS Console → EC2 → Launch Instance
        - Choose Ubuntu Server
        - Select t2.micro or t3.micro (if it is free trial)
        - Create/download a .pem key
        - Open ports:
            -22 (SSH)
            -80 (HTTP)
        - Click launch instance
        
        copy the example path from ssh client

    Why
        -EC2 provides a virtual server
        -Security Group allows browser and SSH access

Step 2: Connect to EC2 using SSH
        - Go to the file where ssh.pm file is present
        - open terminal  
        - add the shh code which we had coped from the ssh client
        -ssh -i keyname.pem ubuntu@<EC2-PUBLIC-IP>

    Why

        -SSH gives secure remote access to the EC2 server
        -ubuntu is the default user for Ubuntu AMI

Download files from the internet directly into the server.
    cammond 
        wget -O app.zip "file url"

Step 3: Update the system
        - sudo apt update

    Why
        -Updates package information
        Prevents installation issues

Step 4: Install Nginx Web Server
        -sudo apt install nginx -y
    Why
        -Nginx serves web pages to users
        -Lightweight and fast for static websites

Step 5: Start and Enable Nginx
        -sudo systemctl start nginx
        -sudo systemctl enable nginx
    Why
        -start runs Nginx immediately
        -enable starts Nginx automatically after reboot

        or
step 3,4,5 in single code
        -sudo apt update && sudo apt install nginx -y / =>install zip zipnginx
        -unzip file.zip


Step 6: Upload Website Files
        -From local machine
        -scp -i keyname.pem -r website/* ubuntu@<EC2-PUBLIC-IP>:/tmp
    Why
        -Transfers website files from local system to EC2

Step 7: Move Files to Web Root
        -sudo rm -rf /var/www/html/*
        -sudo cp -r /tmp/* /var/www/html/
        -sudo chown -R www-data:www-data /var/www/html
                or
        -sudo cp-r ./path/* /var/www/html/
    Why
        -/var/www/html is Nginx default directory
        -Proper ownership avoids permission errors

Step 8: Reload Nginx
        - sudo systemctl reload nginx
    Why
        -Applies changes without stopping the server

Step 9: Access Website
        -Open browser:
        -http://<EC2-PUBLIC-IP>
    Why
        -Public IP allows internet access to your site

If Website Is Not Opening

    Why
        -Check Security Group → HTTP (80) allowed -> shh (20)allowed
        -Check Nginx status:
        -systemctl status nginx
Verify files exist in /var/www/html 

One-Line Interview Answer
        -I hosted a static website on AWS by launching an Ubuntu EC2 instance, installing Nginx, 
        uploading website files to /var/www/html, configuring security groups, and accessing it via 
        public IP.

Interview Questions
    1. What is a static website?
    -A static website contains fixed content like HTML, CSS, JavaScript and does not use server-side processing.

    2. Why use Nginx for hosting static websites?
    -Fast and lightweight
    -  Handles high traffic
    -Easy to configure
    -Low memory usage

    3. What is the default web root of Nginx in Ubuntu?
    -  /var/www/html

    4. What is the role of Security Groups in AWS?
    -Security Groups act as a virtual firewall controlling inbound and outbound traffic to EC2.

    5. Why is port 80 required?
    -Port 80 allows HTTP traffic, which is required to access websites via browser.

    6. What is wget used for?
    -wget is used to download files from the internet directly into the server.

    7. Difference between scp and wget?
    -scp	
        -Copies files from local system
        -Needs SSH
    -wget
        -Downloads files from URL
        -Needs internet

    8. How do you check if Nginx is running?
    -systemctl status nginx

    9. What happens if permissions are wrong?
    -The website may show 403 Forbidden error.

    10. Difference between static and dynamic website?
    -Static	                Dynamic
        -Fixed content	        -Content changes
        -No backend	Uses        -backend (DB, server)
        -Faster	                - Slower




---

Project: Hosting a Static Website on AWS using EC2 & NGINX

#Prfessional Project Explanation (What I Did)

I successfully hosted a **static website on AWS** by launching an **Ubuntu EC2 instance** and 
configuring the **NGINX web server** to serve web content over the internet.
I connected securely to the EC2 instance using **SSH**, installed and configured NGINX, uploaded
website files to the server, and deployed them in the default NGINX web root directory. I also 
configured **AWS Security Groups** to allow HTTP and SSH traffic, enabling public access to the 
website through the EC2 public IP address.

This project demonstrates my understanding of **cloud infrastructure, Linux server management, 
web server configuration, and AWS networking fundamentals**.

---

Key Tasks Performed

* Launched an **Ubuntu EC2 instance**
* Configured **Security Groups** (SSH & HTTP)
* Connected to the server using **SSH**
* Installed and managed **NGINX**
* Uploaded website files using **SCP / Wget**
* Deployed website to `/var/www/html`
* Verified website accessibility using **Public IP**
* Troubleshot common deployment issues

---

Tools & Technologies Used

* AWS EC2
* Ubuntu Linux
* NGINX Web Server
* SSH
* SCP / Wget
* Linux Commands

---

Professional Workflow

```
Launch EC2
→ Configure Security Group
→ Connect via SSH
→ Install NGINX
→ Upload Website Files
→ Deploy to Web Root
→ Reload NGINX
→ Access Website via Public IP
```

---

Resume-Ready Project Description (Short)

> Hosted a static website on AWS by deploying an Ubuntu EC2 instance, configuring NGINX web server,
 managing security groups, and serving web content via public IP.

---

Resume-Ready Project Description (Detailed)

> Designed and deployed a static website on AWS using an Ubuntu EC2 instance. Installed and 
configured NGINX as the web server, securely accessed the instance via SSH, uploaded website files, and exposed the application to the internet using AWS security group rules.

---

Interview Questions & Answers (Professional + Easy)

---

1. Can you explain your project briefly?

**Answer:**
I hosted a static website on AWS by launching an Ubuntu EC2 instance, installing NGINX, deploying website files to the NGINX web root directory, and accessing the site using the EC2 public IP.

---

2. What is a static website?

**Answer:**
A static website contains fixed content such as HTML, CSS, and JavaScript and does not require server-side processing or databases.

---

3. Why did you use NGINX?

**Answer:**
NGINX is lightweight, fast, consumes less memory, and efficiently handles static content and high traffic.

---

4. What is the role of EC2 in your project?

**Answer:**
EC2 provides the virtual server where the operating system, web server, and website files are hosted.

---

5. What is the purpose of a Security Group?

**Answer:**
A Security Group acts as a virtual firewall that controls inbound and outbound traffic to the EC2 instance.

---

6. Why did you open port 80?

**Answer:**
Port 80 is required to allow HTTP traffic so users can access the website through a web browser.

---

7. Why is port 22 required?

**Answer:**
Port 22 is required for SSH access to securely connect and manage the EC2 instance.

---

8. What is the default web root directory of NGINX in Ubuntu?

**Answer:**

```
/var/www/html
```

---

9. What is the use of `wget`?

**Answer:**
`wget` is used to download files directly from the internet to the server.

---

10. Difference between `scp` and `wget`?

| SCP                             | Wget                       |
| ------------------------------- | -------------------------- |
| Copies files from local machine | Downloads files from a URL |
| Uses SSH                        | Uses HTTP/HTTPS            |
| Requires local files            | Requires internet access   |

---

11. How do you check if NGINX is running?

**Answer:**

```bash
systemctl status nginx
```

---

12. What happens if file permissions are wrong?

**Answer:**
The website may show errors like **403 Forbidden** because NGINX cannot access the files.

---

13. How do you fix a website not opening issue?

**Answer:**

* Check Security Group (port 80 allowed)
* Check NGINX status
* Verify files exist in `/var/www/html`

---

14. Difference between static and dynamic websites?

| Static        | Dynamic                 |
| ------------- | ----------------------- |
| Fixed content | Content changes         |
| No backend    | Uses backend & database |
| Faster        | Slightly slower         |

---

One-Line Interview Answer (Final)

> I hosted a static website on AWS by launching an Ubuntu EC2 instance, configuring NGINX, uploading website files to the NGINX web root, and exposing it to the internet using security groups and a public IP.

---




