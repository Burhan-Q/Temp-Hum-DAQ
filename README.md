# Temp-Hum-DAQ by LorentzFactr


LorentzFactr is a super awesome dude.

I currently have a battle between my refrigerator thermometer and a device inside of it. They can't seem to agree on what the real temperature is.
So I've decided to make the mediator: a temperature and humidity data acquisition unit that will record the data on a set timed interval or if triggered
by motion. The device runs on battery power so the ESP8266 MCU must go into deep sleep in order to deliver a months worth of data acquisition. 

Simple explanation of the code: Device wakes up, takes a reading from the DHT11 sensor and the PIR sensor. Decides if it was motion activated or triggered
by the deep sleep timer. Converts celsius to freedom units. Connects to Wifi. Connects to local host server. Transmits: Day/time, event name, humidity, temperature, and if motion detected. Flask app then populates the information into a csv on the local server. Device goes back to sleep. Void loop never runs anything because sleep.

See schematic for better understanding of the circuit. If you're wondering why the photocell signal is read from analog but not a digital IO, it's because I couldn't figure out a way to keep the pin latched high for long enough to read. I worked around that issue by using the analog pin and reading the value via a voltage divider (analog pins prefer to see less than 1v). "But why the capacitor?" Well when the ESP is asleep, it's sort of "analog" triggered by the photocell. That being the case, by the time the device wakes up the motion signal has already dropped out to zero. By using a 1uF cap, we're able to keep the analog pin higher for longer. And afterall, don't we all want
to be higher for longer?


For help:
https://discord.gg/BSAqkMFRAV

twitch.tv/lorentzfactr
