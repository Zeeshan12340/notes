# splunk201
```text-plain
index=botsv1 sourcetype=stream:http dest_ip="192.168.250.70" http_method=POST
```

```text-plain
index=botsv1 sourcetype=stream:http dest_ip="192.168.250.70" http_method=POST uri="/joomla/administrator/index.php" form_data=*username*passwd* | table _time uri src_ip dest_ip form_data
```

Regex:

```text-plain
index=botsv1 sourcetype=stream:http dest_ip="192.168.250.70" http_method=POST form_data=*username*passwd* | rex field=form_data "passwd=(?<creds>\w+)"  | table _time src_ip uri http_user_agent creds
```

```text-plain
index=botsv1 sourcetype=stream:http dest_ip="192.168.250.70" "part_filename{}"="3791.exe"
```

For the evidence of execution, we can leverage sysmon and look at the EventCode=1 for program execution.

```text-plain
index=botsv1 "3791.exe" sourcetype="XmlWinEventLog" EventCode=1
```