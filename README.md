[![logosmallestd](https://user-images.githubusercontent.com/28115284/28752842-881291c0-7546-11e7-9277-bd89186ca933.png)](https://github.com/ersanyamarya)

# Kapacitor_TickScript

### TICKscript Language
Kapacitor is a data processing engine. It can process both stream and batch data. This guide will walk you through both workflows and teach you the basics of using and running a Kapacitor daemon.

* Kapacitor uses a DSL named TICKscript. The DSL is used to define the pipelines for processing data in Kapacitor.
* The TICKscript language is an invocation chaining language. Each script has a flat scope and each variable in the scope defines methods that can be called on it. These methods come in two flavors.
	* Property methods – Modifies the node they are called on and returns a reference to the same node.
	* Chaining methods – Creates a new node as a child of the node they are called on and returns a reference to the new node.

Every TICKscript will have either a stream or batch variable defined depending on the type of task you want to run. The stream and batch variables are an instance of a StreamNode or SourceBatchNode respectively.		
		
##### Pipelines
* Kapacitor uses TICKscripts to define data processing pipelines. A pipeline is set of nodes that process data and edges that connect the nodes. Pipelines in Kapacitor are directed acyclic graphs (DAGs) meaning each edge has a direction that data flows and there cannot be any cycles in the pipeline.
* Each edge has a type, one of the following:
	* StreamEdge – an edge that transfers data a single data point at a time.
	* BatchEdge – an edge that transfers data in chunks instead of one point at a time.
	* MapReduceEdge – this is special case where the data being transfered is unique to the specific map reduce job.

When connecting nodes the TICKscript language will not prevent you from connecting edges of the wrong type but rather the check will be performed at runtime. So just be aware that a syntactically correct script may define a pipeline that is invalid.
	
##### This repository contains Instalation guide, examples of Tick Scripts and their explaination. 

### Example : 
```
stream
    .eval(lambda: "errors" / "total")
        .as('error_percent')
    // Write the transformed data to InfluxDB
    .influxDBOut()
        .database('mydb')
        .retentionPolicy('myrp')
        .measurement('errors')
        .tag('kapacitor', 'true')
        .tag('version', '0.2')
```
***
go to the [wiki](https://github.com/ersanyamarya/Kapacitor_TickScript/wiki) for more information
***

