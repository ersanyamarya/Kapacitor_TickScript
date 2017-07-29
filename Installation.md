# Installation

Requirements

Installation of the InfluxDB package may require root or administrator privileges in order to complete successfully.
#### Networking
Kapacitor listens on TCP port 9092 for all API and write calls.

Kapacitor may also bind to randomized UDP ports for handling of InfluxDB data via subscriptions.

#### Installation
Kapacitor has two binaries:
>kapacitor – a CLI program for calling the Kapacitor API.
>kapacitord – the Kapacitor server daemon.



#### Install InfluxDB and Kapacitor

The instructions below are based on the [official documentation](https://docs.influxdata.com/influxdb/v1.3/introduction/installation/)

* First, configure the package sources.
* Make sure you’ve previously used sudo in the current session, so that the sudo in the command below does not prompt you for a password again. To make sure, you can just run “sudo ls” and check that it doesn’t prompt for a password.

copy + pase + run this :

	curl -sL https://repos.influxdata.com/influxdb.key | sudo apt-key add -	
	source /etc/lsb-release 
	echo "deb https://repos.influxdata.com/${DISTRIB_ID,,} ${DISTRIB_CODENAME} stable" | sudo tee /etc/apt/sources.list.d/influxdb.list

run :

	sudo apt-get update && sudo apt-get install influxdb &&  sudo apt-get install kapacitor
You can also download InfluxDB and Kapacitor from [here](https://portal.influxdata.com/downloads), but I woul recomend to use the above method.
#### Linux - SysV or Upstart Systems
To start the Kapacitor service, run:

	sudo service kapacitor start
#### Linux - systemd Systems

To start the Kapacitor service, run:

	sudo systemctl start kapacitor
