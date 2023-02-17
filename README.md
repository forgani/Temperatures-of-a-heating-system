## Temperatures-of-a-heating-system
Measurement of flow/return temperatures of a heating system with **SONOFF devices** and **Home Assistant**.


I used Sonoff because they are all in one with power supply and box. But before we use them, we should know some important details about them.
The device will not boot into its regular operating mode if GPIO02 is pulled low at boot and so the GPIO02 is useless.<br>
I’m using GPIO03 (Rx) for DS18B20 temperature sensors, which does not have any boot function restrictions.<br><br>

The GPIO14 is definitely not connected (Sonoff Basic R2 V1.0) so I soldered a wire to the chip to access the GPIO14

The rain board module uses a voltage comparator LM393 and the result is given to output in two formats, digital (0 and 1) and analog AO<br>
Remove the Sonoff BASIC cover and desolder the relay and add buzzer with a 220 ohm series resistor instead.<br>
The DS18B20 are "onewire" bus sensors. So we connecting all of the DS18B20s in parallel, sharing all of the VDD, GND and signal pin.<br>
Next we connect signal pins to digital pin GPIO03 (RX) on the Sonoff.<br>

Temperature Sensors are wired according to the following scheme.<br>
The 4.7 kOhm resistor be soldered between the signal pin and VCC.<br>

![grafik](https://user-images.githubusercontent.com/25223934/210085025-c59d339a-22b3-4f3e-8111-159204b9ddbb.png)


In order to get the address, simply start the firmware on your device with a configured dallas hub and observe the log output (the log level must be set to at least debug!).<br>

 
 ![grafik](https://user-images.githubusercontent.com/25223934/210084998-d4a4117d-c1bf-4770-a3e5-a77a26f51bdf.png)


Some specifics about the code:<br>

* The water sensor exposes the entity binary_sensor. that becomes on if a water leak is detected by the sensor’s probe.
* The automation trigger is based on the changing state (on / off) of this entity.
* The notification message will be sent to your smartphone via the alarm_stream to be sure the vibrate/silent ringer mode won’t avoid your device to ring.

 more info: [heating-temperature-monitoring](https://www.forgani.com/electronics-projects/heating-temperature-monitoring/)
