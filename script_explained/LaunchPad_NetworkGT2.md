# TICK SCRIPT - LaunchPad_NetworkGT2

Defining the database retention policy and measurement on which this tick script will be applied.
```
var db = 'dataghost'
var rp = 'two_hours'
var measurement = 'launchpad'
```
Name and id of the Kapacitor Task you want
```
var name = 'LaunchPad_NetworkGT2'
//creating the id name followed by group name
var idVar = name + ':{{.Group}}'
```

Defining thde databse where the outup alerts will be save
```
var outputDB = 'meta'
var outputRP = 'autogen'
var outputMeasurement = 'alerts'
```
Defining the parameters for the alert condition
```
var triggerType = 'relative'

var shift = 5m
var crit = 2
```

Reading a stream
```
var data = stream
    |from()
        .database(db)
        .retentionPolicy(rp)
        .measurement(measurement)
    |eval(lambda: "Network_Strength")
        .as('value')
// Now and onwards the field (Network Strength) will be know as value
```
Create a new node that shifts the incoming points in time.

```
var past = data
    |shift(shift)

```
Create a new node that saves the incoming points in time.
```
var current = data
```
Create a new node that joins the data from both the previous nodes an evaluates a function to "value"
```
var trigger = past
    |join(current) // Joining past and current
        .as('past', 'current')
    //evaluating the % change
    |eval(lambda: abs(float("current.value" - "past.value")) / float("past.value") * 100.0)
        .keep()
        .as('value') // saving it as value
    |alert() //generating alert
        .crit(lambda: "value" > crit) //critical limit 
        .stateChangesOnly() //send alerts only when the state is changed
        // creating the message 
        .message('Alert: Network Change > 2%
			Read at:  {{.Name}}
			Network Strength:  {{ index .Fields "value" }}') 
        .id(idVar)
        //sending it through Telegram App
        .telegram()
```
Saving the alert to the database for future refference
```
trigger
    |influxDBOut()
        .create()
        .database(outputDB)
        .retentionPolicy(outputRP)
        .measurement(outputMeasurement)
        .tag('alertName', name)
        .tag('triggerType', triggerType)
```