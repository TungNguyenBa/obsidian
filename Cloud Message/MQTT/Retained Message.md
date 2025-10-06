1. MQTT normally (no retained)
	When 1 client **publish** 1 message to topic, broker will:
	- Send this message **only for clients that are subscribing to that topic at that time** 
	- Then the message disappears - the broker doesn't save anything
2. Retained message
	Retained message = message is retained by broker after it is published
	When you send 1 message have **flag** -> retain = true, broker will:
	1. **Save message final** for that topic
	2. When any client subscribes to that topic later, the broker will automatically send this retained message immediately.
	Ex:
	- No retained:
		`Publisher: publish("home/temperature", "25^C")
		`Subscriber: (not connected)
		`-> Subscriber connect later: NO received anything`
	- Retained:
		`Publisher: publish("home/temperature", "25^C", retain=True)`
		`Subscriber: (is connected later)`
		`-> Subscriber: Receive message "25°C" immediately`