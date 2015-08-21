
# About this Tutorial
This tutorial explains and how to use the Thing Description (TD) and its minimal vocabulary set. As example, an LED lamp will be modeled with the TD using the JSON-LD format. 


## Basics about Thing Description
The TD is mainly based on the entities Metadata, Data, and the 3 interaction models Property, Action, and Event. 


![TDL Model](TDL.jpg)


### Metadata 
Metadata is used to provide some generic information which may not that relevant at runtime. There are 3 mandatory vocabularies defined within the Metadata:

* Name: Name of the Thing
* Protocol: Which kind of protocols is supported (e.g., HTTP, CoAP, XMPP, etc,)
* Encoding: Which kind of serialization format is supported (e.g., JSON, XML, etc.)

Note: Besides of this 3 defined vocabularies additional characteristics can be defined such as product id, firmware version, location, etc..

### Data 
This field is used to define application specific data types that are used of the interaction models (property, action, event). 

Per default, a subset of XML Schema simple data types are supported which includes string, int, float, byte, short, boolean, unsignedByte, unsignedShort, unsignedInt, and hexBinary (=byte array).

An input or output data field can be assigned as empty which is equivalent to 'void' or 'null'.

### Property

The interaction variant Property is used to serve properties of a Thing which can be static and/or dynamic (e.g., temperature value, fill level of water, etc.).

There are 3 mandatory vocabularies defined within the Property:

* Name: Name of the property
* OutputData: Which data type is associated with this property
* Writeable: Is this property writeable (true/false).

Note: If the property is writeable=true, then the property accept inputData which have the same data type as defined by the outputData.  

### Action
The interaction variant Action invokes actions on a Thing which may or may not result in state change (e.g., move robot, brew cup of coffee, etc).

There are 3 mandatory vocabularies defined within the Action:

* Name: Name of the action
* InputData: Which input data is associated with this action
* OutputData: Which output data is associated with this action

### Event
The interaction variant Event enables an intention to be notified from the Thing on a certain condition. 
There are 2 mandatory vocabularies defined within the Event:

* Name: Name of the action
* OutputData: Which data is associated with this event

Note: Event can also be seen as a Property with abilitiy for subscribtion. 

## Sample Thing: LED Lamp 
A LED Lamp �MyLED� has following characteristics:
* supports CoAP and HTTP as application protocol
* supports only JSON as exchange data format
* can be switched on / off (ledOnOff) using a boolean value (true=On, false=Off)
* provides the color temperature (colorTemperature) in unsignedShort; color temperature can be changed by a client 
* provides current rgb values (red, green, blue) each of them in unsignedByte
* notifies when color temperate is changed (colorTemperatureChanged)

Bringing this in the Thing Description context, we would categorize this information in the following way

##### Metadata
* Name = "MyLED"
* Protocol = CoAP and HTTP
* Encoding = JSON

##### Property
1) 
* Name =  "colorTemperature"
* OutputData = unsignedShort
* Writeable= true

2)
* Name =  "rgbValueRed"
* OutputData = unsignedByte
* Writeable= false

3)
* Name =  "rgbValueGreen"
* OutputData = unsignedByte
* Writeable= false

4)
* Name =  "rgbValueBlue"
* OutputData = unsignedByte
* Writeable= false

##### Action
* Name =  "ledOnOff"
* InputData = boolean
* OutputData = void/null

##### Event
* Name =  "colorTemperatureChanged"
* OutputData = unsignedShort

This can be transformed into JSON-LD representation.

