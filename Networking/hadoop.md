# hadoop
Keytabs are magical things. Think of them as a Kerberos Key. Essentially, you are storing all the information required (including the password) to authenticate in a file. Keytabs can be generated by interfacing with the Kerberos server and executing the following command:

`ktpass /pass <Krb Password> /mapuser <Krb Username> /out <ex.keytab> /princ <username>/<hostname>@<example.com> /ptype KRB5_NT_PRINCIPAL /crypto RC4-HMAC-NT /Target example.` 

[https://kb.iu.edu/d/aumh](https://kb.iu.edu/d/aumh) 

**klist:**

The klist command can be used to gather information from a keytab, since cat'ing the keytab usually ends badly for your shell. We can use the following command to output the principals stored in the keytab file:

`klist -k <keytabfile>`  
  
**kinit:**

The kinit command can be used to use a keytab, authenticate to the Kerberos server, and request a ticket. We can use the following command:

`kinit <principal name> -k -V -t <keytabfile>`  
  
[https://github.com/wavestone-cdt/hadoop-attack-library](https://github.com/wavestone-cdt/hadoop-attack-library)