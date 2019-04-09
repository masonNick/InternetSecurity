# Internet Security
My project for CS445 - Internet Security, will be focused on embedding self-created certificates to the trusted Cas list. I will attempt to provide functional implementation and a detailed report on how it works, explaining key concepts.

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
  - Looking into openSSL certificate creation, including creating both a public and private key for my program. 
  - The use of the openssl/x509.h and the openssl/rsa.h header files will allow me to do this. 
  - The openssl/x509.h file will let me generate a private key dynamically, while the openssl/rsa.h will allow me to create a RSA key. 
  - Finally, I will attempt to create the certificate itself by using the X509 struct to show a x509 certificate in the memory. The basis for this struct is located within the openssl/x509.h header file. 
  - Using, X509_new, creates a dynamically allocated struct, used for the certificate creation.
  - Code example for the certificate: 
    - X509 * certificate;              //Creating the certificate pointer of type X509.
    - certificate = X509_new();        //Dynamically creating the certificate.
- 4/8/2019
  - Self creating a SSL certificate creator is beneficial locally on your computer for encryption, as well as publically on the Internet through the use of various web browsers, including Google Chrome, Internet Explorer, and Apple's Safari.
  - These private use SSL certificates allows a given user protection to various attacks from hackers, including at least a "Man in the Middle Attack."
  - There will be five steps that I will attempt to follow: 
    - Step 1: Create a RSA Keypair
    - Step 2: Extract the Private Key into an “httpd” Folder
    - Step 3: Creating a “Certificate Signing Request” or CSR File
    - Step 4: Creating the Certificate “.crt” File
    - Step 5: Configuring Apache to Use the Files

**Helpful References**
- https://www.netburner.com/learn/creating-a-self-signed-certificate-for-secure-iot-applications/
- file:///Users/nicholasmason/Desktop/UNR/CS445-NicholasMason-Project.html
- https://www.openssl.org/docs/manmaster/man3/X509_new.html
- https://stackoverflow.com/questions/256405/programmatically-create-x509-certificate-using-openssl
- https://www.rosehosting.com/blog/how-to-generate-a-self-signed-ssl-certificate-on-linux/
