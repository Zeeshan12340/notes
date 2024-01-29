# dns zone transfer
We will perform DNS zone transfer using the Microsoft tool is  nslookup.exe

Once we execute it, we provide the DNS server that we need to ask, which in this case is the target machine

Now let's try the DNS zone transfer on the domain we find in the AD environment. To add records use the following syntax

```text-plain
dig windcorp.thm any @$IP
```

```text-plain
dig @10.10.175.182 ironcorp.me axfr
```

```text-plain
nslookup.exe
> server 10.10.144.35
> ls -d thmredteam.com
```

use `nsupdate` to add insecure txt records manually

```text-plain
> server 10.10.10.10
> update add test.windcorp.thm 5 TXT "Don't mind me.."
> send
> update delete selfservice.windcorp.thm
> send
> update add selfservice.windcorp.thm 86400 A 192.168.16.53
> send
```

BreachingAD:
------------

To configure a custom dns we can use `nmcli` as follows:

```text-plain
nmcli con mod tun0 ipv4.dns "10.200.24.101 1.1.1.1"
systemctl restart NetworkManager
```

where `10.200.24.101` is the ip of the domain controller dns. `1.1.1.1` is added to ensure you still have internet access.