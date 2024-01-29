# PS Downgrade
The PowerShell downgrade attack is a very low-hanging fruit that allows attackers to modify the current PowerShell version to remove security features.

Most PowerShell sessions will start with the most recent PowerShell engine, but attackers can manually change the version with a one-liner. By "downgrading" the PowerShell version to 2.0, you bypass security features since they were not implemented until version 5.0.

The attack only requires a one-liner to execute in our session. We can launch a new PowerShell process with the flags `-Version` to specify the version (2).

```text-plain
PowerShell -Version 2
```

The two easiest mitigations are removing the PowerShell 2.0 engine from the device and denying access to PowerShell 2.0 via application blocklisting.

```text-plain
[Ref].Assembly.GetType('System.Management.Automation.AmsiUtils').GetField('amsiInitFailed','NonPublic,Static').SetValue($null,$true)
```

First, the snippet will call the reflection function and specify it wants to use an assembly from `[Ref.Assembly]` it will then obtain the type of the AMSI utility using `GetType`.

```text-plain
[Ref].Assembly.GetType('System.Management.Automation.AmsiUtils')
```

The information collected from the previous section will be forwarded to the next function to obtain a specified field within the assembly using `GetField`.

```text-plain
.GetField('amsiInitFailed','NonPublic,Static')
```

The assembly and field information will then be forwarded to the next parameter to set the value from `$false` to `$true` using `SetValue`.

```text-plain
.SetValue($null,$true)
```

Once the `amsiInitFailed` field is set to `$true`, AMSI will respond with the response code: AMSI\_RESULT\_NOT\_DETECTED = 1

Patching AMSI:
--------------

`AmsiScanBuffer` is vulnerable because `amsi.dll` is loaded into the PowerShell process at startup; our session has the same permission level as the utility.

At a high-level AMSI patching can be broken up into four steps,

1.  Obtain handle of `amsi.dll`
2.  Get process address of `AmsiScanBuffer`
3.  Modify memory protections of `AmsiScanBuffer`
4.  Write opcodes to `AmsiScanBuffer`