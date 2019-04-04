# Internet Security
My project for CS445 - Internet Security, will be focused on embedding self-created certificates to the trusted Cas list. I will attempt to provide implementation of this functionality and a detailed report on how it works, explaining key concepts.

**To do list**
- (1) Code Implementation 
- (2) Documentation and Technical Report

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
  - Looking into openSSL certificate creation, including creating both a public and private key for my program. The use of the openssl/x509.h and the openssl/rsa.h header files will allow me to do this. The openssl/x509.h file will let me generate a private key dynamically, while the openssl/rsa.h will allow me to create a RSA key.

**Helpful References**
- https://www.netburner.com/learn/creating-a-self-signed-certificate-for-secure-iot-applications/
- file:///Users/nicholasmason/Desktop/UNR/CS445-NicholasMason-Project.html
