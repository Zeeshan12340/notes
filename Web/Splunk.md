# Splunk
Metadata Command:
-----------------

```text-plain
| metadata type=sourcetypes index=botsv2 | eval firstTime=strftime(firstTime,"%Y-%m-%d %H:%M:%S") | eval lastTime=strftime(lastTime,"%Y-%m-%d %H:%M:%S") | eval recentTime=strftime(recentTime,"%Y-%m-%d %H:%M:%S") | sort - totalCount
```

Filter command for botsv3:

```text-plain
index="botsv3" hash | stats count by sourcetype | sort -count
| tstats count where index="botsv3" by sourcetype
```

Index:  
       We first specify index as `index=botsv1` and also the domain in plaintext

Src:  
       Going to "src" tag we see the IPs in our data

       we specify src parameter in our search and also sourcetype so the overall command becomes

       `index=botsv1 imreallynotbatman.com src=40.80.148.42 sourcetype=suricata`

Stats:  
       We use stats feature to count the src\_ip and sort with requests(custom defined param)

       `index=botsv1 imreallynotbatman.com sourcetype=stream* | stats count(src_ip) as Requests by src_ip | sort - Requests` (NICE FOR FILTERING MOST WEB TRAFFIC IP)  
       (web scanner Acunetix)

Sourcetype:  
       specify http stream source type to see web requests

       `index=botsv1 src=40.80.148.42 sourcetype=stream:http`

       We can tell the destination IP as

       `dest="192.168.250.70"`  
       `index=botsv1 sourcetype=stream:http dest="192.168.250.70" http_method=POST form_data=*username*passwd* | table form_data`

Tables:  
       use  `table _time form_data | reverse` to show time in table form and reverse shows the first password request(apparantly)

Regex:  
       Use regex pattern to match password  
       `| rex field=form_data "passwd=(?<userpassword>\w+)" | eval lenpword=len(userpassword)`

Lookups:  
       We can add lookups but unnecessary at this point imo

       `| stats avg(mylen) AS avg_len_http| eval avg_len_http=round(avg_len_http,0)`

Time(transaction):  
       `| transaction userpassword | table duration`  
Count:  
       `| stats dc(userpassword)`  
MD5:  
       `index=botsv1 3791.exe CommandLine=3791.exe | stats values(MD5)`

Downloaded files:  
       `index=botsv1 sourcetype=stream:http src=192.168.250.100 | stats count values(url) by dest`  
       `index=botsv1 sourcetype=XmlWinEventLog:Microsoft-Windows-Sysmon/Operational host=we8105desk EventCode=2  TargetFilename="C:\\Users\\bob.smith.WAYNECORPINC\\*.txt" | stats dc(TargetFilename)`

       `index=botsv1 sourcetype=*win* pdf dest=we9041srv.waynecorpinc.local Source_Address=192.168.250.100 | stats dc(Relative_Target_Name)`  
 

**Splunk2**
-----------

 To remove duplicates use `| dedup site<keyword>` , and for tables `| table site<keyword>`

```text-plain
index="botsv2" sourcetype="stream:http"  10.0.2.101 *beer* | dedup site | table site
index="botsv2" src_ip="45.77.65.211" uri_path="/member.php"
index="botsv2"  sourcetype="stream:http" source="stream:httpbrewertalk" "<script>" kevin
```

search in form\_data field for sqli

```text-x-csrc
index="botsv2" host="MACLORY-AIR13" (*.ppt OR *.pptx) 
index="botsv2" kutekitten earliest="08/03/2017:18:18:07" latest="08/03/2017:18:19:07" 
index="botsv2" sourcetype="stream:ftp" method=RETR (for files downloaded with winsys32.dll)
index="botsv2" 45.77.65.211 sourcetype="stream:http" source="stream:http"
```