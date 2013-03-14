JXML, revision 0
================

JXML is a loss-less representation of JSON in XML, so data can be reused with XML tools.
JXML is based on JSONx (See http://goo.gl/I3cxs for details). 

JXML syntax features uniform nodes to allow simpler encoders and decoders.
JXML syntax provides smaller XPATH queries and smaller XML files. 
JXML syntax is subject to change.

Conversion guide
================

JSON identifiers are represented by the string contents in the type:name attribute.
Type is represented by a single character and is mandatory. 
Name is optional. Most Unicode characters are valid within identifiers, as long as they are properly escaped (for example, \unnnn). 

JSON boolean
If the JSON boolean has a property name transformation becomes <j son="b:name"></j>, else becomes <j son="b"></j>. The boolean value is character data as either true or false. JSON boolean sample ("remote": false) transforms into JXML boolean (<j son="b:remote">false</j>)

JSON string
If the JSON string has a property name transformation becomes <j son="s:name"></j>, else becomes <j son="s"></j>. The string value is character data. JSON string sample ("name":"John Smith") transforms into JXML string (<j son="s:name">John Smith</j>)

JSON number
If the JSON number has a property name transformation becomes <j son="n:name"></j>, else becomes <j son="n"></j>. The number value is character data. JSON number sample ("height": 62.4) transforms into JXML number (<j son="n:height">62.4</j>)

JSON null
If the JSON null value has a property name transformation becomes <j son="0:name" />, else becomes <j son="0" />. JSON null value sample ("additionalInfo": null) transforms into JXML null value (<j son="0:additionalInfo" />)

JSON object
If the JSON object has a property name transformation becomes <j son="o:name"></j>, else becomes <j son="o"></j>. The value of the object depends on its type. JSON object sample ({ "Ticker" : "IBM" }) transforms into JXML object (<j son="o"><j son="s:Ticker">IBM</j></j>)

JSON array
If the JSON array has a property name transformation becomes <j son="a:name"></j>, else becomes <j son="a"></j>. The value of the array depends on its type. Array elements are ordered according to their document order. JSON array sample ("phoneNumbers": [ "212 555-1111", "212 555-2222" ]) transforms into JXML array (<j son="a:phoneNumbers"><j son="s">212 555-1111</j><j son="s">212 555-2222</j></j>)

Root element
The root element is either an JXML object or a JXML array element.

Special characters
JSON escaped characters in strings might become character entity references. 
Any strings escaped with \u becomes XML entity references specified in decimal. 
\b (backspace) is not supported in XML and, subsequently, is not supported in JXML.

JXML sample
===========

The following example document is a sample of the JSON structure.

{
  "name":"John Smith",
  "address": {
    "streetAddress": "21 2nd Street",
    "city": "New York",
    "state": "NY",
    "postalCode": 10021,
  },
  "phoneNumbers": [
    "212 555-1111",
    "212 555-2222"
  ],
  "additionalInfo": null,
  "remote": false,
  "height": 62.4,
  "ficoScore": " > 640"
}

The following output is the result of the transformed document to JXML.

<?xml version="1.0" encoding="UTF-8"?>
<j son="o">
    <j son="s:name">John Smith</j>
    <j son="o:address">
        <j son="s:streetAddress">21 2nd Street</j>
        <j son="s:city">New York</j>
        <j son="s:state">NY</j>
        <j son="n:postalCode">10021</j>
    </j>
    <j son="a:phoneNumbers">
        <j son="s">212 555-1111</j>
        <j son="s">212 555-2222</j>
    </j>
    <j son="0:additionalInfo" />
    <j son="b:remote">false</j>
    <j son="n:height">62.4</j>
    <j son="s:ficoScore">&gt; 640</j>
</j>

Credits
=======

JXML was created by Mario "rlyeh" Rodriguez.
JSONx is an IBM® standard format to represent JSON as XML.
This document includes text written by IBM guys. Thanks guys :D

