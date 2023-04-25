# Sonoff-Zigbee-Bridge-Pro-for-HA
I have 25+ Sonoff kit flashed with Tasmota in my Home Assistant installation.
One of the major pieces of plant that I use HA to supervise is my "whole of house" Vallox ventillation system.
This monitors the condition of the air centrally and in the event that it detects higher humidity it boosts the ventilation rate.
This is OK but because it is reactive and because the airflow through one bathroom is quite small compared to thte whole house, it means that the bathromm can become fairly steamy before the ventilation speeds up. I had set up a sonoff mini2 behind a retractive switch outside the bathroom which fired a mqtt message off to increase the flow rate before showering. Although this worked technically it wasn't very good, because it was easy to forget. I was considered moving the retractive switch into the bathroom but this would have involved redecoratinf AND I also learnt that the "volts free" contacts on the Sonoff Mini2 are actually floating at 110Vwhich means that 
a didn't work devices that I use I wanted to use IKEA tradfi buttons Getting Sonoff ZB Pro ready to run ZHA with Tasmota 12.5
Normal Tasmo process
solder in headre
Use webflasher as 32-bit
Add template
Run script 1
run cscript 2
autoconfig
instal zha
https://notenoughtech.com/home-automation/tasmota-on-sonoff-zb-bridge-pro/
https://dialedin.com.au/blog/sonoff-zbbridge-p-setup
