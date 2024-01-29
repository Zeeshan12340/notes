# Nmap
`nmap -S SPOOFED_IP MACHINE_IP`

`sudo nmap -sS -p80 -f 10.20.30.144 where -f fragments request to try to bypass firewall/IDS`

for zombie scan, i.e, using another idle machine to scan your target machine, use

You can also set Nmap to use random source IP addresses instead of explicitly specifying them. By running `nmap -sS -Pn -D RND,RND,ME -F MACHINE_IP`, Nmap will choose two random source IP addresses to use as decoys. Nmap will use new random IP addresses each time you run this command. In the screenshot below, we see how Nmap picked two random IP addresses in addition to our own, `10.14.17.226`.

`nmap -sS -Pn --proxies PROXY_URL -F MACHINE_IP`

Nmap scan with the fixed source TCP port number 8080. We have used the following Nmap command, `nmap -sS -Pn -g 8080 -F MACHINE_IP`.

`nmap -sS -Pn --ttl 81 -F 10.10.238.22`

### Relying on Source Routing

In many cases, you can use source routing to force the packets to use a certain route to reach their destination. Nmap provides this feature using the option `--ip-options`. Nmap offers loose and strict routing:

*   Loose routing can be specified using `L`. For instance, `--ip-options "L 10.10.10.50 10.10.50.250"` requests that your scan packets are routed through the two provided IP addresses.
*   Strict routing can be specified using `S`. Strict routing requires you to set every hop between your system and the target host. For instance, `--ip-options "S 10.10.10.1 10.10.20.2 10.10.30.3"` specifies that the packets go via these three hops before reaching the target host.

Set IP options

Nmap lets you control the value set in the IP Options field using `--ip-options HEX_STRING`, where the hex string can specify the bytes you want to use to fill in the IP Options field. Each byte is written as `\xHH`, where `HH` represents two hexadecimal digits, i.e., one byte.

A shortcut provided by Nmap is using the letters to make your requests:

*   `R` to record-route.
*   `T` to record-timestamp.
*   `U` to record-route and record-timestamp.
*   `L` for loose source routing and needs to be followed by a list of IP addresses separated by space.
*   `S` for strict source routing and needs to be followed by a list of IP addresses separated by space.

`--badsum,` `You can use this to your advantage to discover more about the systems in your network`

|     |     |
| --- | --- |
| **Port Scan Type** | **Example Command** |
| TCP Null Scan | `sudo nmap -sN 10.10.67.68` |
| TCP FIN Scan | `sudo nmap -sF 10.10.67.68` |
| TCP Xmas Scan | `sudo nmap -sX 10.10.67.68` |
| TCP Maimon Scan | `sudo nmap -sM 10.10.67.68` |
| TCP ACK Scan | `sudo nmap -sA 10.10.67.68` |
| TCP Window Scan | `sudo nmap -sW 10.10.67.68` |
| Custom TCP Scan | `sudo nmap --scanflags URGACKPSHRSTSYNFIN 10.10.67.68` |
| Spoofed Source IP | `sudo nmap -S SPOOFED_IP 10.10.67.68` |
| Spoofed MAC Address | `--spoof-mac SPOOFED_MAC` |
| Decoy Scan | `nmap -D DECOY_IP,ME 10.10.67.68` |
| Idle (Zombie) Scan | `sudo nmap -sI ZOMBIE_IP 10.10.67.68` |
| Fragment IP data into 8 bytes | `-f` |
| Fragment IP data into 16 bytes | `-ff` |

`nmap  -sI <idle machine IP> <target IP>`

`nmap -sS --traceroute 10.10.209.134`

`nmap -sV --version-light 10.10.209.134 for version checking`

|     |     |
| --- | --- |
| Script Category | Description |
| `auth` | Authentication related scripts |
| `broadcast` | Discover hosts by sending broadcast messages |
| `brute` | Performs brute-force password auditing against logins |
| `default` | Default scripts, same as `-sC` |
| `discovery` | Retrieve accessible information, such as database tables and DNS names |
| `dos` | Detects servers vulnerable to Denial of Service (DoS) |
| `exploit` | Attempts to exploit various vulnerable services |
| `external` | Checks using a third-party service, such as Geoplugin and Virustotal |
| `fuzzer` | Launch fuzzing attacks |
| `intrusive` | Intrusive scripts such as brute-force attacks and exploitation |
| `malware` | Scans for backdoors |
| `safe` | Safe scripts that won’t crash the target |
| `version` | Retrieve service versions |
| `vuln` | Checks for vulnerabilities or exploit vulnerable services |