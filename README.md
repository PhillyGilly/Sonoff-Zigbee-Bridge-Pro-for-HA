# Sonoff-Zigbee-Bridge-Pro-for-HA
I have 25+ Sonoff units all flashed with Tasmota working over wifi in my Home Assistant installation.
One of the major pieces of plant that I use HA to supervise is my "whole of house" Vallox ventillation system.
This monitors the condition of the air centrally and in the event that it detects higher humidity it boosts the ventilation rate.
This is OK but because it is reactive and because the airflow through one bathroom is quite small compared to thte whole house, it means that the bathromm can become fairly steamy before the ventilation speeds up. I had set up a sonoff mini2 behind a retractive switch outside the bathroom which fired a mqtt message off to increase the flow rate before showering. Although this worked technically it wasn't very good, because it was easy to forget. I was considered moving the retractive switch into the bathroom but this would have involved redecoratinf AND I also learnt that the "volts free" contacts on the Sonoff Mini2 are actually floating at 110V which means that it's not the kind of thing you want to be near when wet and naked!
At the same time I had seen the IKEA tradfi buttons being used in other home automation applications. They are small, light, relatively cheap, neat, harmless and waterproof to IP44. So I decided to make a forray into Zigbee, however due to the distance between my Raspberry Pi and my bathrooms and the structure of my house a USB dongle wouldn't be suitable, so I selected the Sonoff Zigbee Bridge Pro as a remote controller. Finally compatibility issues about the IKEA buttons meant that I was going to be using Zigbee2MQTT add-on.
The instructions set out here provided a pretty good stating point.
https://notenoughtech.com/home-automation/tasmota-on-sonoff-zb-bridge-pro/
However I found that the Tasmota on-line flasher is easier to use.
https://tasmota.github.io/install/
Apart from that just kee fololowing not-enough-tech's instuctions.
You don't need to upload any file or re-size the parttion because unter tha latest Tasmota 12.5 it's all done for you.
Just run the two Berry console scripts. The second one takes about 5 minutes so be very patient.
When you re-boot the bridge you will now be able to see that it will work as a Zigbee co-ordinator.
However this is where you need to go back to the main menu and select configuaration then auto-configuration and configure the bridge for TCP.
![image](https://user-images.githubusercontent.com/56273663/234308947-d2d1088f-4871-4b1a-afae-7fad94e845ed.png)

Normal Tasmo process
solder in headre
Use webflasher as 32-bit
Add template
Run script 1
run cscript 2
autoconfig
instal zha

https://dialedin.com.au/blog/sonoff-zbbridge-p-setup
