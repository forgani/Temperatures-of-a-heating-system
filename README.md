# Temperatures-of-a-heating-system
Measurement of flow/return temperatures of a heating system with SONOFF devices and Home Assistant.

The device will not boot into its regular operating mode if GPIO02 is pulled low at boot.
I’m using GPIO03 (Rx) for DS18B20 temperature sensors, which does not have any boot function restrictions.

The GPIO14 is definitely not connected (Sonoff Basic R2 V1.0) so I solder a wire to the chip to access the GPIO14
Connect Sonoff device for Esphome install

Complete ESPHome Installation Guide: 4 different ways to install ESPHome

Connect USB FTDI programmer to the computer, hold down the basic broad button to connect GPIO0 to GND while the device is booting to put it in Programming and Flash mode.
Note: We supply USB power to Sonoff via FTDI and make sure you set 3.3V setting on FTDI, 5V will cause damage.

    3x DS18B20 temperature Sensor
    moisture sensor (3.3V-5V) binary leakage sensor
    1x 4.7k Ohms Resistor

The rain board module uses a voltage comparator LM393 and the result is given to output in two formats, digital (0 and 1) and analog AO

Using With Sonoff Basic — ESPHome

    Open ESPHome Interface and click on the New Device button.
    Enter device name of your choice as well as your WiFi name and password.
    In the next dialog, click on Pick specific Board radio button and select the Generic ESP8266 (for example Sonoff) click Next button.
    lick Install button and you will have ESPHome installed on your ESP device

If everything is fine, a terminal will appear with a lot of text and multiple text based progress bars.
When the ESP installation is finished, your new ESPHome device will be automatically added in the ESPHome Dashboard.

Temperature Sensors are wired according to the following scheme.
The 4.7 kOhm resistor be soldered between the signal pin and VCC.

![grafik](https://user-images.githubusercontent.com/25223934/210085025-c59d339a-22b3-4f3e-8111-159204b9ddbb.png)


Getting Sensor IDs

In order to get the address, simply start the firmware on your device with a configured dallas hub and observe the log output (the log level must be set to at least debug!).
Note that you don’t need to define the individual dallas sensors just yet, as the scanning will happen even with no sensors connected.

 
 ![grafik](https://user-images.githubusercontent.com/25223934/210084998-d4a4117d-c1bf-4770-a3e5-a77a26f51bdf.png)

# Note you don't have to add any sensors at this point

Now we can add the individual sensors to our configuration:
Some specifics about the code above

    The water sensor exposes the entity binary_sensor. that becomes on if a water leak is detected by the sensor’s probe.
    The automation trigger is based on the changing state (on / off) of this entity.
    The notification message will be sent to your smartphone via the alarm_stream to be sure the vibrate/silent ringer mode won’t avoid your device to ring.

 more info: https://www.forgani.com/electronics-projects/heating-temperature-monitoring/
