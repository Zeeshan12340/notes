# ssh
for using ssh anywhere on the internet, simply forward the ssh port with ngrok(need to setup an account to get access token),

or you can forward the ssh port to a non-conventional one, too with

```text-plain
socat tcp-l:<other port>,fork,reuseaddr tcp:<IP>:22
ngrok tcp localhost:<other port>
```

then simply ssh with 

```text-plain
ssh -oStrictHostKeyChecking=no -oUserKnownHostsFile=/dev/null -p <ngrok-port> zeeshan@<number>.tcp.in.ngrok.io
```

the `-oStrictHostKeyChecking=no -oUserKnownHostsFile=/dev/null` flags aren't needed but help simplify the connection.

```text-plain
SSH -oHostKeyAlgorithms=+ssh-dss root@10.10.xx.xx
```