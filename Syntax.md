[![logosmallestd](https://user-images.githubusercontent.com/28115284/28752842-881291c0-7546-11e7-9277-bd89186ca933.png)](https://github.com/ersanyamarya)

# Syntax

#### Literals
****
**Booleans**

* Boolean literals are the key words TRUE and FALSE. They are case sensitive.

**Numbers**

* Numbers are typed and are either a float64 or an int64. If the number contains a decimal it is considered to be a float64 otherwise it is an int64. All float64 numbers are considered to be in base 10. If an integer is prefixed with a 0 then it is considered a base 8 (octal) number, otherwise, it is considered base 10.

Valid number literals:
#### Literals
****
**Booleans**

* Boolean literals are the key words TRUE and FALSE. They are case sensitive.

**Numbers**

* Numbers are typed and are either a float64 or an int64. If the number contains a decimal it is considered to be a float64 otherwise it is an int64. All float64 numbers are considered to be in base 10. If an integer is prefixed with a 0 then it is considered a base 8 (octal) number, otherwise, it is considered base 10.

Valid number literals:

    1 	int64
    1.2	float64
    5	int64
    5.0	float64
    0.42	float64
    0400	octal int64

**Strings**

* There are two ways to write string literals:
	* Single quoted strings with backslash escaped single quotes.
	 This string `'single \' quoted'` becomes the literal `single ' quoted`.
	* Triple single quoted strings with no escaping.
	This string `'''tri
ple \' quoted'''` becomes the literal `triple \' quoted`.

**Durations**

* TICKscript supports durations literals. They are of the form of InfluxQL duration literals. See https://docs.influxdata.com/influxdb/v1.3/query_language/spec/#literals
* Duration literals specify a length of time. An integer literal followed immediately (with no spaces) by a duration unit listed below is interpreted as a duration literal.
* **Duration unit definitio
ns**
```
Units 		Meaning
u or µ 		microseconds (1 millionth of a second)
ms 		milliseconds (1 thousandth of a second)
s 		second
m 		minute
h 		hour
d 		day
w 		week
```
* **Statements**

* A statement begins with an identifier and any number of chaining function calls. The result of a statement can be assigned to a variable using the var keyword and assignment operator =.

Example:
```
var errors = stream
    |from()
        .measurement('errors')
var requests = stream
    |from()
    .measurement('requests')
// Join the errors and requests stream
errors
    |join(requests)
        .as('errors', 'requests')
    |eval(lambda: "errors.value" / "requests.value")
```
#### Format
***

**Whitespace**

* Whitespace is ignored and can be used to format the code as you like.

* Typically property methods are indented in from their calling node. This way methods along the left edge are chaining methods.

For example:
```
stream
    |eval(lambda: "views" + "errors")
        .as('total_views') // Increase indent for property method.
    |httpOut('example') // Decrease indent for chaining method.
```
**Comments**

* Ba
    1 	int64
    1.2	float64
    5		int64
    5.0	float64
    0.42	float64
    0400	octal int64

**Strings**

* There are two ways to write string literals:
	* Single quoted strings with backslash escaped single quotes.
	 This string `'single \' quoted'` becomes the literal `single ' quoted`.
	* Triple single quoted strings with no escaping.
	This string `'''tri
ple \' quoted'''` becomes the literal `triple \' quoted`.

**Durations**

* TICKscript supports durations literals. They are of the form of InfluxQL duration literals. See https://docs.influxdata.com/influxdb/v1.3/query_language/spec/#literals
* Duration literals specify a length of time. An integer literal followed immediately (with no spaces) by a duration unit listed below is interpreted as a duration literal.
* **Duration unit definitions**
```
Units 		Meaning
u or µ 		microseconds (1 millionth of a second)
ms 		milliseconds (1 thousandth of a second)
s 		second
m 		minute
h 		hour
d 		day
w 		week
```
* **Statements**

* A statement begins with an identifier and any number of chaining function calls. The result of a statement can be assigned to a variable using the var keyword and assignment operator =.

Example:
```
var errors = stream
    |from()
        .measurement('errors')
var requests = stream
    |from()
    .measurement('requests')
// Join the errors and requests stream
errors
    |join(requests)
        .as('errors', 'requests')
    |eval(lambda: "errors.value" / "requests.value")
```
#### Format
***

**Whitespace**

* Whitespace is ignored and can be used to format the code as you like.

* Typically property methods are indented in from their calling node. This way methods along the left edge are chaining methods.

For example:
```
stream
    |eval(lambda: "views" + "errors")
        .as('total_views') // Increase indent for property method.
    |httpOut('example') // Decrease indent for chaining method.
```
**Comments**

* Basic // style single line comments are supported.