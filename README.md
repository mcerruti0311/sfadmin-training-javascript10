# sfadmin-training-javascript10

## What You'll Learn in This Hour
```
* What JSON is
* How to simulate associative arrays
* About JSON and objects
* Accessing JSON data
* Data serialization with JSON
* How to keep JSON secure
```
## Meet JSON
Earlier in the book you saw how to directly
instantiate an object using the new Object()
syntax. In this hour you learn about
** JavaScript Object Notation ** (JSON), which,
as its name implies, offers another way to
create object instances, and which can also
act as a general-purpose data exchange
syntax.

### Note
```
The official home of JSON is at
 http://json.org/, which also has links to a
  wide variety of JSON resources on the Web.
```
## What Is JSON?
JSON (pronounced “Jason”) is a simple and compact notation for JavaScript
objects. Once expressed in JSON, objects can easily be converted to strings to
be stored and transmitted (across networks or between applications, for
instance).

However, the real beauty of JSON is that an object expressed in JSON is really
just expressed in normal JavaScript code. You therefore take advantage of
“automatic” parsing in JavaScript; you can just have JavaScript interpret the
contents of a JSON string as code, with no extra parsers or converters.

## JSON Syntax
JSON data is expressed as a sequence of parameter and value pairs, each pair
using a colon character to separate parameter from value. These
`"parameter":"value"` pairs are themselves separated by commas:

`"param1":"value1", "param2":"value2", "param3":"value3"`

Finally, the whole sequence is enclosed between curly braces to form a JSON
object representing your data:
```JavaScript
var jsonObject = {
    "param1":"value1",
    "param2":"value2",
    "param3":"value3"
}
```
The object jsonObject defined here uses a subset of standard JavaScript
notation—it’s just a little piece of valid JavaScript code.

Objects written using JSON notation can have properties and methods accessed
directly using the usual dot notation:

`alert(jsonObject.param1); // alerts 'value1'`

More generally, though, JSON is a general-purpose syntax for exchanging data in
a string format. Not only objects, but ANY data that can be expressed as a
series of `parameter:value` pairs can be expressed in JSON notation. It is then
easy to convert the JSON object into a string by a process known as
serialization; serialized data is convenient for storage or transmission around
networks. You’ll see how to serialize a JSON object later in this hour.

### Note
```
As a general-purpose data exchange syntax, JSON can be used somewhat like XML,
though JSON can be simpler for humans to read. Also, the parsing of large XML
files can be a slow process, whereas JSON gives your script a JavaScript
object, ready to use.
```

JSON has gathered momentum recently because it offers several important
advantages. JSON is

* Easy to read for both people and computers
* Simple in concept—a JSON object is nothing more than a series of
`parameter:value` pairs enclosed by curly braces
* Largely self-documenting
* Fast to create and parse
* A subset of JavaScript, meaning that no special interpreters or other
additional packages are necessary

A number of leading online services and APIs including Flickr, Twitter, and
several services from Google and Yahoo! now offer data encoded using JSON
notation.

### Note
```
See http://www.flickr.com/services/api/response.json.html for details of how
Flickr supports JSON.
```
## Accessing JSON Data
To recover the data encoded into the JSON string, you need to somehow convert
the string back to JavaScript code. This is usually referred to as *deserializing*
the string.

## Using eval()
Only more recent browsers have native support for JSON syntax (we talk about
using native browser support in just a moment). However, since JSON syntax is
a subset of JavaScript, the JavaScript function eval() can be used to convert
a JSON string into a JavaScript object.

The `eval()` function uses the JavaScript interpreter to parse the JSON text and
produce a JavaScript object:

`var myObject = eval ('(' + jsonObjectString + ')');`

You can then use the JavaScript object in your script:

``` JavaScript
var user = '{"username" : "philb1234","location" : "Spain","height" : 1.80}';
var myObject = eval ('(' + user + ')');
alert(myObject.username);
```

### Note
```
The JavaScript eval() function evaluates or executes whatever is passed as an
argument. If the argument is an expression, eval() evaluates the expression;
for example,

var x = eval(4 * 3); // x=12

If the argument comprises one or more JavaScript statements, eval() executes
those statements:

eval("a=1; b=2; document.write(a+b);"); // writes 3 to the page
```

### Caution
```
The string must be enclosed in parentheses like this to avoid falling foul of an
ambiguity in the JavaScript syntax.
```
## Using Native Browser Support
All recent browsers offer native support for JSON, making the use of `eval()`
unnecessary.

Browsers with native JSON support create a JavaScript object called `JSON` to
manage JSON encoding and decoding. The `JSON` object has two methods,
`stringify()` and `parse()`.

### Note
```
Browsers natively supporting JSON include

* Firefox (Mozilla) 3.5+
* Internet Explorer 8+
* Google Chrome
* Opera 10+
* Safari 4+
```

### JSON.parse()
You can interpret a JSON string using the method `JSON.parse()`, which takes a
string containing a JSON-serialized object and breaks it up, creating an object
with properties corresponding to the `"parameter":"value"` pairs found in the
string:
```JavaScript
var Mary = '{ "height":1.9, "age":36, "eyeColor":"brown" }';
var myObject = JSON.parse(Mary);
var out = "";
for (i in myObject) {
    out += i + " = " + myObject[i] + "\n";
}
alert(out);
```
You can see the result in Figure 10.1.

![10fig01.jpg](images\10fig01.jpg)

**Figure 10.1** Using `JSON.parse()`

## Data Serialization with JSON
In the context of data storage and transmission, *serialization* is the name
given to the process of converting data into a format that can be stored or
transmitted across a network and recovered later into the same format as the
original.

In the case of JSON, a string is the chosen format of the serialized data. To
serialize your JSON object (for instance, to send it across a network
connection), you need to express it as a string.

In later browsers, those having JSON support, you can simply use the
`JSON.stringify()` method.

### JSON.stringify()
You can create a JSON-encoded string of an object using the `JSON.stringify()`
method.

Let’s create a simple object and add some properties:
```JavaScript
var Dan = new Object();
Dan.height = 1.85;
Dan.age = 41;
Dan.eyeColor = "blue";
```
Now you can serialize the object using `JSON.stringify`:

`alert( JSON.stringify(Dan) );`

The serialized object is shown in Figure 10.2.

![10fig02.jpg](images\10fig02.jpg)

**FIGURE 10.2** Using `JSON.stringif()`

## JSON Data Types
The parameter part of each `parameter:value` pair must follow a few simple
grammatical rules:

* It must not be a JavaScript reserved keyword.
* It must not start with a number.
* It must not include any special characters except the underscore or dollar sign.

The values in JSON objects can contain any of the following data types:

* Number
* String
* Boolean
* Array
* Object
* null (empty)

### Caution
```
JavaScript syntax has several data types that are not included in the JSON
standard, including Date, Error, Math, and Function. These data types must be
represented as some other data format, with the encoding and decoding programs
following the same encoding and decoding rules.
```
## Simulating Associative Arrays
