# Getting Started

#### Writing the Tick Script

* create a file with the task name followed by ".tick"
`eg: sample_task.tick `
* save the file

#### Parts of Tick Script
* Reading the data

Batch eg: -
```
	var data = stream
    	|from()
        	.database(db)
        	.retentionPolicy(rp)
        	.measurement(measurement)
```
Stream eg: -
```
	batch
  	|query('''SELECT * FROM "db"."retentionPolicy"."measurement"''')
    	.period(1s)
    	.every(1s)
```
* Manupulating the data 

eg: -
```
var past = data
    	|shift(shift)
```
* Performing joins or other operations

eg: -

```
var trigger = past
	|join(data)
	.as('past', 'current')
```
* Generating alerts
	* defining the Lambda function
	* defining the message
	* declearing the output node
	
eg: -
```
|alert()
        .crit(lambda: "value" > crit)
        .stateChangesOnly()
        .message(message)
        .id(idVar)
        .telegram()
```
* Generating Triggers
	* saving alerts to database
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
#### Adding task with the Tick Script
Type thin in the CLI
```
kapacitor define  <task name> 
-type <stream/batch> 
-tick <tick script> 
-dbrp <database>.<retention policy>
```
See the list of tasks : `kapacitor list tasks`

To enable a tasks : `kapacitor enable <task name>`

