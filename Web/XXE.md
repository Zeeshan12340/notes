# XXE
XML (eXtensible Markup Language) is a markup language that defines a set of rules for encoding documents in a format that is both human-readable and machine-readable. It is a markup language used for storing and transporting data.

Every XML document mostly starts with what is known as XML Prolog.  
  
`<?xml version="1.0" encoding="UTF-8"?>`

DTD stands for Document Type Definition. A DTD defines the structure and the legal elements and attributes of an XML document.

`<!DOCTYPE note [ <!ELEMENT note (to,from,heading,body)> <!ELEMENT to (#PCDATA)> <!ELEMENT from (#PCDATA)> <!ELEMENT heading (#PCDATA)> <!ELEMENT body (#PCDATA)> ]>`

So now let's understand how that DTD validates the XML. Here's what all those terms used in `note.dtd` mean

*   !DOCTYPE note -  Defines a root element of the document named **note**
*   !ELEMENT note - Defines that the note element must contain the elements: "to, from, heading, body"
*   !ELEMENT to - Defines the `to` element to be of type "#PCDATA"
*   !ELEMENT from - Defines the `from` element to be of type "#PCDATA"
*   !ELEMENT heading  - Defines the `heading` element to be of type "#PCDATA"
*   !ELEMENT body - Defines the `body` element to be of type "#PCDATA"

    **NOTE**: #PCDATA means parseable character data.

`<?xml version="1.0" ?>`  
`<!DOCTYPE foo [ <!ELEMENT foo ANY >`  
`<!ENTITY xxe SYSTEM "file:///etc/passwd">]>`

`<root><name>`  
`aa`  
`</name><tel>aa</tel><email>&xxe;</email><password>aa</password></root>`