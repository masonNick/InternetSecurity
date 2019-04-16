# Internet Security
My project for CS445 - Internet Security, will be focused on embedding self-created certificates. In addition, I will attempt to add these self-signed certificates to the trusted CAS list. I will attempt to provide functional implementation and a detailed report on how it works, explaining key concepts.
- By: Nicholas Mason
- Due: April 28th, 2019

**To do list**
- (1) Code Implementation 
- (2) Research
- (3) Documentation and Technical Report

**Day to Day Progress**
- 3/26/2019 
  - Looking into how to write a program to create a self assigned certificate to secure a given website. Research on what it takes to complete this task, and looking into sudo commands.
  - I updated and uploaded a technical report overview and formatting to github.
- 3/28/2019
  - Starting technical report section on SSL certificates and Certificate Authorities.
- 4/2/2019
  - Working on HTML website that I will give a certificate to show it is secure. 
  - file:///Users/nicholasmason/Desktop/UNR/CS445-NicholasMason-Project.html
- 4/3/2019
  #### Looking into openSSL certificate creation, including creating both a public and private key for my program. 
      - The use of the openssl/x509.h and the openssl/rsa.h header files will allow me to do this. 
      - The openssl/x509.h file will let me generate a private key dynamically. 
      - The openssl/rsa.h will allow me to create a RSA key. 
      - Finally, I will attempt to create the certificate itself by using the X509 struct to show a x509 certificate in the memory. 
        - The basis for this struct is located within the openssl/x509.h header file. 
      - Using, X509_new, creates a dynamically allocated struct, used for the certificate creation.
  #### Code example for the certificate: 
      - X509 * certificate;              //Creating the certificate pointer of type X509.
      - certificate = X509_new();        //Dynamically creating the certificate.
- 4/8/2019
  - Self creating a SSL certificate creator is beneficial locally on your computer for encryption, as well as publically on the Internet through the use of various web browsers, including Google Chrome, Internet Explorer, and Apple's Safari.
  - These private use SSL certificates allows a given user protection to various attacks from hackers, including at least a "Man in the Middle Attack."
  #### There will be five steps that I will attempt to follow: 
      - Step 1: Create SSL Certificate
        - Step 1.5: Configure Apache Webserver
      - Step 2: Configure Apache to Use SSL Certificate
      - Step 3: Adjust the firewall and Chnaging Features in Apache
      - Step 4: Test the Newly Created Encryption
      - Step 5: Changing to Permanent Redirect
- 4/9/2019
  - Working on my technical report. Updated technical report uploaded to GitHub.
  - Looking into how to take self-signed certificate and add it to the trusted CAS list.
  
- 4/15/2019
  - Working on code implementation 
  #### Step 1: Create SSL Certificate
    NOTE: I will do this using the openssl tool downloaded in the terminal in Linux. 
    ##### Type the following to generate a RSA private key, with length 2048 bits long modulus.
      ~$ sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/apache-selfsigned.key -out /etc/ssl/certs/apache-selfsigned.crt
    ##### The creator of the certificate will be asked a series of questions: 
      Country Name (2 letter code) [AU]:US
      State or Province Name (full name) [Some-State]:Nevada
      Locality Name (eg, city) []:Sparks
      Organization Name (eg, company) [Internet Widgits Pty Ltd]:Nick Mason
      Organizational Unit Name (eg, section) []: CS445
      Common Name (e.g. server FQDN or YOUR name) []:IP Address
      Email Address []:myEmailAddress@domainName
  #### Step 1.5: Configure Apache Webserver
      ~$ sudo apt update
      ~$ sudo apt install apache2 
    - This will install apache onto your Linux machine. 
    ##### You should be able to start your apache webserver by typing: 
      ~$ sudo systemctl status apache2
    - Now, using your server IP address, you can go see that your apache webserver is indeed up and running. You can change the contents displayed on the apache webserver by altering the index.html file associated with your webserver. 
    ##### Type: 
      http:// <IP address of server> 
     
  #### Step 2: Configure Apache to Use SSL Certificate
     ##### (1) I will build a configuration snippet in order to create secure the default SSL settings.
       ~$ sudo nano /etc/apache2/conf-available/ssl-params.conf
    ##### (2) I will alter the included SSL Apache Virtual Host file in order to point to my newly created SSL certificates from Step 1.
    ##### (3) I will alter the unencrypted Virtual Host file to automatically redirect requests to the encrypted Virtual Host.

- 4/16/2019
  #### Step 3: Adjust the firewall and Chnaging Features in Apache
  
  #### Step 4: Test the Newly Created Encryption
  
  #### Step 5: Changing to Permanent Redirect
     
**Helpful References**
- https://www.netburner.com/learn/creating-a-self-signed-certificate-for-secure-iot-applications/
- https://www.openssl.org/docs/manmaster/man3/X509_new.html
- https://stackoverflow.com/questions/256405/programmatically-create-x509-certificate-using-openssl
- https://www.rosehosting.com/blog/how-to-generate-a-self-signed-ssl-certificate-on-linux/
- https://www.namecheap.com/support/knowledgebase/article.aspx/798/67/what-is-an-rsa-key-used-for
- https://unix.stackexchange.com/questions/90450/adding-a-self-signed-certificate-to-the-trusted-list
- https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-apache-in-ubuntu-18-04
- https://www.bounca.org/tutorials/install_root_certificate.html
