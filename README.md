Milkcocoa Arduino SDK
=====

[Milkcocoa](https://mlkcca.com/) SDK for Arduino & ESP8266.

Works with the ESP8266 Arduino platforms, and anything that supports Arduino's Client interface.


## How To Use

Include library(`#include <Milkcocoa.h>`), and write a code like below.

```
//client is Ethenet Client
Milkcocoa milkcocoa = Milkcocoa(&client, MQTT_SERVER, MILKCOCOA_SERVERPORT, MILKCOCOA_APP_ID, MQTT_CLIENTID); 

void setup() {
 	//"on" API was able to call in setup
	milkcocoa.on("milkcocoa_datastore_name", "push", onpush);
}

void loop() {
	//milkcocoa.loop must be called in loop()
	milkcocoa.loop();

	//push
	DataElement elem = DataElement();
	elem.setValue("name", "Milk");
	elem.setValue("age", 35);
	milkcocoa.push("milkcocoa_datastore_name", elem);

	delay(10000);
}

void onpush(DataElement elem) {
  Serial.println(elem.getString("name"));
  Serial.println(elem.getInt("age"));
  // Output:
  // Milk
  // 35
};
```


## Examples

- [Simple ESP8266 Example](https://github.com/milk-cocoa/Milkcocoa_Arduino_SDK/blob/master/examples/milkcocoa_esp8266/milkcocoa_esp8266.ino): simple test of `push()` and `on("push")`.
- [ESP8266 TOUT Example](https://github.com/milk-cocoa/Milkcocoa_Arduino_SDK/blob/master/examples/milkcocoa_esp8266_tout/milkcocoa_esp8266_tout.ino): get sensor data from TOUT of ESP8266
