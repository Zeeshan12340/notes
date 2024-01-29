# AMSI Bypass
The  [CLR (**C**ommon **L**anguage **R**untime)](https://docs.microsoft.com/en-us/dotnet/standard/clr)  and  [DLR (**D**ynamic **L**anguage **R**untime)](https://docs.microsoft.com/en-us/dotnet/framework/reflection-and-codedom/dynamic-language-runtime-overview)  are the runtimes for .NET and are the most common you will encounter when working with Windows systems.

A runtime detection measure will scan code before execution in the runtime and determine if it is malicious or not. Depending on the detection measure and technology behind it, this detection could be based on string signatures, heuristics, or behaviors. If code is suspected of being malicious, it will be assigned a value, and if within a specified range, it will stop execution and possibly quarantine or delete the file/code.

AMSI will determine its actions from a response code as a result of monitoring and scanning. Below is a list of possible response codes,

![](AMSI%20Bypass/29a13a3e9b0d64542dc9951a49ddda.png)

*   AMSI\_RESULT\_CLEAN = 0
*   AMSI\_RESULT\_NOT\_DETECTED = 1
*   AMSI\_RESULT\_BLOCKED\_BY\_ADMIN\_START = 16384
*   AMSI\_RESULT\_BLOCKED\_BY\_ADMIN\_END = 20479
*   AMSI\_RESULT\_DETECTED = 32768

![](AMSI%20Bypass/35e16d45ce27145fcdf231fdb8dcb3.png)