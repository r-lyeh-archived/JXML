<pre>
JXML, revision 0
================

JXML is a loss-less representation of JSON in XML, so data can be reused with XML tools.
JXML is based on JSONx (See http://goo.gl/I3cxs for details). 

JXML syntax features a single uniform node 'j'. Tree iteration through XPath indices is possible.
JXML syntax provides small XPath queries and relatively tiny XML files. 
JXML syntax is subject to change.

Conversion guide
================

JSON identifiers are represented by the string contents in the type:name attribute.
- Type is required. It is represented by a single character (see below). 
- Name is optional. 

Special characters
JSON escaped characters in strings might become character entity references. 
Most Unicode characters are valid within identifiers, as long as they are properly escaped (for example, \unnnn). 
Any strings escaped with \u becomes XML entity references specified in decimal. 
\b (backspace) is not supported in XML and, subsequently, is not supported in JXML.

JSON boolean
If the JSON boolean has a property name transformation becomes &lt;j son="b:name"&gt;&lt;/j&gt;, else becomes &lt;j son="b"&gt;&lt;/j&gt;. 
The boolean value is character data as either true or false.
JSON boolean sample ("remote": false) transforms into (&lt;j son="b:remote"&gt;false&lt;/j&gt;)

JSON string
If the JSON string has a property name transformation becomes &lt;j son="s:name"&gt;&lt;/j&gt;, else becomes &lt;j son="s"&gt;&lt;/j&gt;. 
The string value is character data. 
JSON string sample ("name":"John Smith") transforms into (&lt;j son="s:name"&gt;John Smith&lt;/j&gt;)

JSON number
If the JSON number has a property name transformation becomes &lt;j son="n:name"&gt;&lt;/j&gt;, else becomes &lt;j son="n"&gt;&lt;/j&gt;. 
The number value is character data. 
JSON number sample ("height": 62.4) transforms into (&lt;j son="n:height"&gt;62.4&lt;/j&gt;)

JSON null
If the JSON null value has a property name transformation becomes &lt;j son="0:name" /&gt;, else becomes &lt;j son="0" /&gt;. 
JSON null value sample ("additionalInfo": null) transforms into (&lt;j son="0:additionalInfo" /&gt;)

JSON object
If the JSON object has a property name transformation becomes &lt;j son="o:name"&gt;&lt;/j&gt;, else becomes &lt;j son="o"&gt;&lt;/j&gt;. 
The value of the object depends on its type. 
JSON object sample ({ "Ticker" : "IBM" }) transforms into (&lt;j son="o"&gt;&lt;j son="s:Ticker"&gt;IBM&lt;/j&gt;&lt;/j&gt;)

JSON array
If the JSON array has a property name transformation becomes &lt;j son="a:name"&gt;&lt;/j&gt;, else becomes &lt;j son="a"&gt;&lt;/j&gt;. 
The value of the array depends on its type. Array elements are ordered according to their document order. 
JSON array sample ("IDs": [ "2-111", "2-222" ]) transforms into (&lt;j son="a:IDs"&gt;&lt;j son="s"&gt;2-111&lt;/j&gt;&lt;j son="s"&gt;2-222&lt;/j&gt;&lt;/j&gt;)

Root element
The root element is either a JXML object or a JXML array element.

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
  "IDs": [
    "2-111",
    "2-222"
  ],
  "additionalInfo": null,
  "remote": false,
  "height": 62.4,
  "ficoScore": "&gt; 640"
}

The following output is the result of the transformed document to JXML.

&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;j son="o"&gt;
    &lt;j son="s:name"&gt;John Smith&lt;/j&gt;
    &lt;j son="o:address"&gt;
        &lt;j son="s:streetAddress"&gt;21 2nd Street&lt;/j&gt;
        &lt;j son="s:city"&gt;New York&lt;/j&gt;
        &lt;j son="s:state"&gt;NY&lt;/j&gt;
        &lt;j son="n:postalCode"&gt;10021&lt;/j&gt;
    &lt;/j&gt;
    &lt;j son="a:IDs"&gt;
        &lt;j son="s"&gt;2-111&lt;/j&gt;
        &lt;j son="s"&gt;2-222&lt;/j&gt;
    &lt;/j&gt;
    &lt;j son="0:additionalInfo" /&gt;
    &lt;j son="b:remote"&gt;false&lt;/j&gt;
    &lt;j son="n:height"&gt;62.4&lt;/j&gt;
    &lt;j son="s:ficoScore"&gt;&amp;gt; 640&lt;/j&gt;
&lt;/j&gt;

Credits
=======

JXML was created by Mario "rlyeh" Rodriguez.
JSONx is an IBM® standard format to represent JSON as XML.
This document includes text written by IBM. Thanks guys! :D
</pre>
