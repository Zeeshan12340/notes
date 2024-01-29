# kerberos certificate
`certutil -v -template > cert_templates.txt`

**Parameter 1: Relevant Permissions**

We need to have the permissions to generate a certificate request in order for this exploit to work. We are essentially looking for a template where our user has either the _**Allow Enroll**_ or _**Allow Full Control**_ permission. You will probably never find a certificate where you have the _Allow Full Control_ permission. However, if you do, congratulations! You can misconfigure the template yourself to make it vulnerable! But for now, let's focus on _Allow Enroll._

It is not as simple as just grepping through the output for the keywords _**Allow Enroll**_ and your AD account, since certificate template permissions are in most cases assigned to AD groups, not directly to AD users. So you will have to grep for all _**Allow Enroll**_ keywords and review the output to see if any of the returned groups match groups that your user belongs to.

**Parameter 2: Client Authentication**

Once we've shortened the list to certificate templates that we are allowed to request, the next step is to ensure that the certificate has the _**Client Authentication**_ EKU. This EKU means that the certificate can be used for Kerberos authentication. There are other ways to exploit certificates, but for this room, this EKU will be the primary focus.

To find these, we need to review the EKU properties of the template and ensure that the words _**Client Authentication**_ is provided. Other templates that do not match this, for now, we can discard.

**Parameter 3: Client Specifies SAN**

Last but definitely not least, we need to verify that the template allows us, the certificate client, to specify the Subject Alternative Name (SAN). The SAN is usually something like the URL of the website that we are looking to encrypt. For example: tryhackme.com. However, if we have the ability to control the SAN, we can leverage the certificate to actually generate a kerberos ticket for any AD account of our choosing!

To find these templates, we grep for the _**CT\_FLAG\_ENROLLEE\_SUPPLIES\_SUBJECT**_ property flag that should be set to 1. This indicates that we can specify the SAN ourselves.

[https://tryhackme.com/room/adcertificatetemplates](https://tryhackme.com/room/adcertificatetemplates) 

`Rubeus.exe asktgt /user:svc.gitlab /enctype:aes256 /certificate:<path to certificate> /password:<certificate file password> /outfile:<name of file to write TGT to> /domain:lunar.eruca.com /dc:<IP of domain controller>`