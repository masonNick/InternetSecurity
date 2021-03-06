# Internet Security
My project for CS445 - Internet Security, will be focused on embedding self-created certificates. In addition, I will attempt to add these self-signed certificates to Firefox. I will attempt to provide functional implementation and a detailed report on how it works, explaining key concepts.
- By: Nicholas Mason
- Due: May 10th, 2019
__________________________________________________________________________________________________________________________________________
### About my Project
__________________________________________________________________________________________________________________________________________
### Components to my Project:
  ##### (1) Githib README.md
    This is used to show the code segments used to accomplish my goal.
  ##### (2) Technical Report
    The technical report is added as a PDF and Word Document in my InternetSecurity Github Page. 
  ##### NOTE: I show my daily progress of what I have done. It includes the dates and what I researched. 
__________________________________________________________________________________________________________________________________________

**To do list**
- (1) Code Implementation 
  - Part 1: Creating Self-Signed Certificate
  - Part 2: Adding my Self-Signed Certificate to Firefox
- (2) Research
- (3) Documentation and Technical Report
__________________________________________________________________________________________________________________________________________

**Day to Day Progress**
- 3/26/2019 
  - Looking into how to write a program to create a self-signed certificate to secure a given website. Research on what it takes to complete this task, and looking into sudo commands.
  - I updated and uploaded a technical report overview and formatting to github.
- 3/28/2019
  - Starting technical report section on SSL certificates and Certificate Authorities.
- 4/2/2019
  - Working on technical report.
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
  - Self creating a SSL certificate creator is beneficial locally on your computer for encryption, as well as publically securing data on the Internet through the use of various web browsers, including Google Chrome, Internet Explorer, and Apple's Safari.
  - These private use SSL certificates allows a given user protection to various attacks from hackers, including at least a "Man in the Middle Attack."
__________________________________________________________________________________________________________________________________________
### Main Method Used for My Project.
__________________________________________________________________________________________________________________________________________
### Part 1: Creating Self-Signed Certificate
__________________________________________________________________________________________________________________________________________
  #### There will be five steps that I will attempt to follow: 
      - Step 1: Create SSL Certificate
        - Step 1.5: Configure Apache Webserver
      - Step 2: Configure Apache to Use SSL Certificate
      - Step 3: Adjust the firewall and Changing Features in Apache
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
     ##### (1) I will build a configuration snippet in order to secure my the default SSL settings, which will secure my apache webserver once it has gone live. 
       ~$ sudo nano /etc/apache2/conf-available/paramsCS445.conf
     ##### NOTE: I used paramsCS445 as the name of my default SSL settings configuration file that I created. I used standardized parameters used for popular software.
    ##### (2) I will alter the included SSL Apache Virtual Host file in order to point to my newly created SSL certificates from Step 1.
      Note: Use this code to duplicate the original default-ssl.conf configuration file before changing it with the newly created certificate information.
      
      ~$ sudo cp /etc/apache2/sites-available/default-ssl.conf /etc/apache2/sites-available/default-ssl.conf.bak
      
    ##### Original Virtual Host file for the default looks as follows: (I deleted comments for better reading).
      <IfModule mod_ssl.c>
          <VirtualHost _default_:443>
                ServerAdmin webmaster@localhost

                DocumentRoot /var/www/html

                ErrorLog ${APACHE_LOG_DIR}/error.log
                CustomLog ${APACHE_LOG_DIR}/access.log combined

                SSLEngine on

                SSLCertificateFile      /etc/ssl/certs/ssl-cert-snakeoil.pem
                SSLCertificateKeyFile /etc/ssl/private/ssl-cert-snakeoil.key

                <FilesMatch "\.(cgi|shtml|phtml|php)$">
                                SSLOptions +StdEnvVars
                </FilesMatch>
                <Directory /usr/lib/cgi-bin>
                                SSLOptions +StdEnvVars
                </Directory>

          </VirtualHost>
      </IfModule>
    ##### Modify the Virtual Host File to include the new ServerAdmin name and include ServerName. In addition, on the SSLCertificateFile and SSLCertificateKeyFile, alter it to include the path with the newly created crt file and key file.
      <IfModule mod_ssl.c>
          <VirtualHost _default_:443>
                ServerAdmin myEmailAddress@domainName                             //Change email
                ServerName IP Address of webserver [Apache Webserver IP address]  //Change IP for Apache

                DocumentRoot /var/www/html

                ErrorLog ${APACHE_LOG_DIR}/error.log
                CustomLog ${APACHE_LOG_DIR}/access.log combined

                SSLEngine on

                SSLCertificateFile      /etc/ssl/certs/apache-selfsigned.crt       //Change to .crt file
                SSLCertificateKeyFile /etc/ssl/private/apache-selfsigned.key       //Change to .key file

                <FilesMatch "\.(cgi|shtml|phtml|php)$">
                                SSLOptions +StdEnvVars
                </FilesMatch>
                <Directory /usr/lib/cgi-bin>
                                SSLOptions +StdEnvVars
                </Directory>

          </VirtualHost>
      </IfModule>
      
    ##### (3) I will alter the unencrypted Virtual Host file to automatically redirect requests to the encrypted Virtual Host.
      ~$ sudo nano /etc/apache2/sites-available/000-default.conf
    ##### In order to make the Apache Webserver more secure, I will alter the traffic of the http to https. This will redirect the traffic from the site to the SSL version of the server. 
      <VirtualHost *:80>
        . . .

        Redirect permanent "/" "https://<Your Apache IP Address for which you are using for your project>/"

        . . .
    </VirtualHost>

- 4/16/2019
  #### Step 3: Adjust the firewall and Changing Features in Apache
    ##### In this section, the user wants to make sure that the firewall will allow for Apache features. Utilizing the ufw command, I can see the available applications that are available in the firewall for Apache Webserver. 
      ~$ sudo ufw app list  //Allows the user to see which applications are available with Apache. 
    ##### I want to make sure that https traffic, as configured in Step 2, part 3, is allowed in these applications. By simply seeing Apache as an available application in your status screen, http is allowed through the firewall. However, https is only allowed if you change the Apache application to Apache Full. You can do this by: 
      ~$ sudo ufw allow 'Apache Full'
      ~$ sudo ufw delete allow 'Apache'
    - By deleting the 'Apache' application and replacing it with 'Apache Full', I am able to let in https traffic to my Apache Webserver I am testing for my project. 
    ##### Finally, we will need to adjust some features in the Apache Webserver in order to use my newly changed and created config files.
    ##### First, type: 
      ~$ sudo a2enmod ssl
      ~$ sudo a2enmod headers
    - The first line will enable the apache module. 
    - The second line enables the mod_headers, which will be used in the newly configured files.
    
    ##### Second, we will enable the SSL virtual-host by typing:
      ~$ sudo a2ensite default-ssl
    ##### Fianlly, we will enable Apache to use our paramsCS445.conf file that we created earlier in the project. Type: 
      ~$ sudo a2enconf paramsCS445
  
  #### Step 4: Test the Newly Created Encryption
  ##### I am able to check if the Apache Webserver is registered under https by typing the following into a web browser. For this example, I am using Firefox, which is built into my Ubuntu Linux 18.04 machine through Virtual Box.
      https://<IP Address of your machine you are working on for this project> 
    - Note: There will still be a message that pops up on your web browser claiming that your server is not secure, forcing the user to click a button, acknowledging that they know that the website is not "private". This will be addressed in the second part of this project, where I attempt to add my self-signed certificate for this Apache Webserver to the Trusted CAS list for Firefox. 
  
  ##### Finally, you will need to restart you Apache Webserver by typing this command into your terminal:
      ~$ sudo systemctl restart apache2
__________________________________________________________________________________________________________________________________________
      
### Part 2: Adding my Self-Signed Certificate to Firefox
__________________________________________________________________________________________________________________________________________
**Adding my Self-Signed Certificate to Firefox**
- The goal of this section is to take our self-signed certificate for our Apache Webserver, created above, and import it into Firefox on my Virtual Machine running Ubuntu 18.04.
- My goals for this section include: 
  - (1) Add my self-signed certificate to the Firefox.
  - (2) Achieve encryption for my apache webserver. 
##### To start: 
    Open Firefox, and go to the settings menu. 
    Navigate your way to the Advanced settings, where the Certificates menu physically resides. 
##### Next, you will need to click on the import tab in the Certificates menu of your Firefox settings. 
    Select the root certificate for your self-signed certificate that was created earlier in this project. 
    I will select all trust levels for the certificate that I have created because I know that it is secure and created by myself. 
    You can view your certificate in the list of certificates your web browser trusts now. 
##### Finally, you will be able to see have encrypted data for your Apache Webserver.
__________________________________________________________________________________________________________________________________________
     
**Helpful References**
- https://www.netburner.com/learn/creating-a-self-signed-certificate-for-secure-iot-applications/
- https://www.openssl.org/docs/manmaster/man3/X509_new.html
- https://stackoverflow.com/questions/256405/programmatically-create-x509-certificate-using-openssl
- https://www.rosehosting.com/blog/how-to-generate-a-self-signed-ssl-certificate-on-linux/
- https://www.namecheap.com/support/knowledgebase/article.aspx/798/67/what-is-an-rsa-key-used-for
- https://unix.stackexchange.com/questions/90450/adding-a-self-signed-certificate-to-the-trusted-list
- https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-apache-in-ubuntu-18-04
- https://www.bounca.org/tutorials/install_root_certificate.html
