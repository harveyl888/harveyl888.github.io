---
layout: article
title: "Towards Lab IoT"
excerpt: "Moving towards IoT in a lab"
categories: blog
created: 2019-10-16
comments: false
share: false
ads: false
---

Chemistry scale-up labs tend to have multiple pieces of equipment connected to a single reactor.  These items can work indepentently, co-dependently or fully-dependently with respect to each other.  Automated reactors have been in existence for a number of years.  These systems can generally collect and store data for a limited number of interfaces and typically work through wired connections.  Here I'm documenting the first step towards a fully-functioning internet-of-things (IoT) lab so that multiple reactors can run processes that may be dependent on one another.  
The final system should allow for the following:

-  unidirectional and bidirectional communication
-  software-managed PID control so that one input can be controlled by another output
-  alarms and failsafes - raise an alarm when out of spec and provide the ability to return to a setpoint
-  continual monitor of connection and checking for disconnect (drop leads to alarm and return to failsage)
-  database to store measurements
-  visualization to monitor data

I settled on a few hardware and software solutions to put this into effect.

### Hardware Solutions
Each instrument can be controlled by a small controller.  The controller should be able to interface with the instrument and publish and receive data.  It should run background code that allows it to react to received data.  It should also communicate wirelessly via wifi and allow ssh communication.  Obvious choice is the Raspberry Pi ZeroW but we could also consider the Adafruit Feather HUZZAH ESP8266 (a little more challenging to add ssh).

### Software Solutions
I chose to implement MQTT as a protocol.  It's a lightweight messaging protocol that runs over TCP/IP.  MQTT works by having clients publish messages through topics to a broker, which manages all the traffic.  Clients can also subscribe to any topics, receiving messages from the broker as they arrive.  This routes all messages through a central location as well as allowing clients to communicate with each other (via the broker).  For IoT data received from multiple sources with time being a key piece of metadata a time series database (in this case InfluxDB) is a suitable choice for data storage.  The data can then be displayed in real-time using grafana.



