# Subdomains
`dnsrecon -t brt -d acmeitsupport.thm`

`ffuf -w /usr/share/seclists/Discovery/DNS/namelist.txt -H "Host: FUZZ.acmeitsupport.thm" -u` [`http://10.10.114.101`](http://10.10.114.101)

`./sublist3r.py -d acmeitsupport.thm`

`site:*.tryhackme.com`