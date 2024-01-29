# sshuttle
```text-plain
sshuttle -e 'ssh -q -o CheckHostIP=no -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null' -r linux-admin@10.200.107.33 0.0.0.0/0 -vv
```