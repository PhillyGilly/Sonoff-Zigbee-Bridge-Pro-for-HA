# Sonoff-Zigbee-Bridge-Pro-for-HA

## Background
I have 25+ Sonoff units all flashed with Tasmota working over wifi in my Home Assistant installation.  One of the major pieces of plant that I use HA to supervise is my "whole of house" Vallox ventillation system.  This monitors the condition of the air centrally and in the event that it detects higher humidity it boosts the ventilation rate. This is OK, but because it is reactive, and because the airflow through one bathroom is quite small compared to the whole house, it means that the bathroom can become fairly steamy before the ventilation speeds up.

I had set up a sonoff mini2 behind a retractive switch outside the bathroom which fired a mqtt message off to increase the flow rate before showering. Although this worked technically it wasn't very good, because it was easy to forget. I was considering moving the retractive switch into the bathroom but this would have involved redecoration AND I also learnt that the "volts free" contacts on the Sonoff Mini2 are actually floating at 110V which means that it's not the kind of thing you want to be near when wet and naked!

At the same time I had seen the IKEA tradfi buttons being used in other home automation applications. They are small, light, relatively cheap, neat, harmless and waterproof to IP44. So I decided to make a forray into Zigbee, however due to the distance between my Raspberry Pi and my bathrooms and the structure of my house a USB dongle wouldn't be suitable, so I selected the Sonoff Zigbee Bridge Pro as a remote controller. Finally compatibility issues about the IKEA buttons meant that I was going to be using Zigbee2MQTT add-on.

## Sonoff Zigbee Bridge Pro
The instructions set out here provided a pretty good stating point and are easy to follow. I don't know why Sonoff don't supply the bridge with the header fitted as providing the pin-outs means they know that users want to modify it. 
https://notenoughtech.com/home-automation/tasmota-on-sonoff-zb-bridge-pro/

The only improvement to thhe procedure abouce is that I prefer the Tasmota on-line flasher as it avoids the step of searching for and downloading it ans then installing and runiining an ESP32 flasher.
https://tasmota.github.io/install/

Once you have got the Bridge to talk to your wifi, set it up with a static IP and remember that for later mine is 19.168.2.110.

Apart from that just keep following not-enough-tech's instuctions.

You can skip all the stuff about uploading files and re-sizing the partion because unter tha latest Tasmota 12.5 it's all done for you.

Just run the two Berry console scripts. The second one takes about 5 minutes, so be very, very, very patient.
When you re-boot the bridge you will now be able to see that it will work as a Zigbee co-ordinator with "Add" and "Map" functions.

However, this is where you need to go back to the main menu and select configuaration then auto-configuration and configure the bridge for TCP.

![image](https://user-images.githubusercontent.com/56273663/234308947-d2d1088f-4871-4b1a-afae-7fad94e845ed.png)

## Zigbee2mqtt
Now head over to HA and install Zigbee2mqtt.

This is a very useful resource https://www.zigbee2mqtt.io/ but this is how I set up my config using edit as YAML
```
data_path: /config/zigbee2mqtt
socat:
  enabled: false
  master: pty,raw,echo=0,link=/tmp/ttyZ2M,mode=777
  slave: tcp-listen:8485,keepalive,nodelay,reuseaddr,keepidle=1,keepintvl=1,keepcnt=5
  options: "-d -d"
  log: true
mqtt:
  server: mqtt://192.168.2.100:1883
  basetopic: zigbee2mqtt
  user: z2m-user
  password: z2m-pass
serial:
  port: tcp://192.168.2.110:8888
ota:
  ikea_ota_use_test_url: false
  update_check_interval: 1440
  disable_automatic_update_check: false
frontend:
  port: 8080
homeassistant: true
zigbee_herdsman_debug: true
```
note: **do not include adapter: ezsp** whatever it says in the instructions.

That's it really. You should be up and running!

![image](https://user-images.githubusercontent.com/56273663/234315595-5bd7bc18-2188-4ab3-8ea7-c872efa20bdb.png)

One final point about updating the firmware on IKEA Tradfri buttons.
You  can do this using the OTA function, but you have to keep pressing the button to keep the button awake until you get confirmation that the OTA update has started. Oh, and you are going to use a lot of battery as it is a very long/slow process.

![image](https://user-images.githubusercontent.com/56273663/234537357-b3986f73-ab8c-4c02-b7c6-58b889c5275e.png)
