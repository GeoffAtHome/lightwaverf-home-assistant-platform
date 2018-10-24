# lightwaverf-home-assistant-platform
Integration of LightwaveRF switches and lights with Home Assistant (HASS) as a platfrom

It's very crude, but does work. It's been working for me for several years with the 1st generation of LightWave kit. I have not tested this with the newer (2nd gen) Lightwave products.

## Caveat
This code may show your devices in the Home Assistant UI, but it may not be able to control the lights for you. The code speaks directly to your Lightwave WiFi Link. Obviously, if you don't have a WiFi Link, then this isn't going to work for you.

## Installation
### Adding the Lightwave Component to Home Assistant
The lightwave files needs to be placed in the installation directory of Home Assistant. For me the final directory looks like
```
/custom_components/light/lightwave.py
/custom_components/switch/lightwave.py
/custom_components/lightwave.py
``` 
There are instructions to follow on the instructions on the home-assistant website. If you need help, let me know.

### Adding LightwaveRF to your configuration file
Now that the component is installed you will need to add the setup to you configuration file.

```
lightwave:
    host: ip_address
```
Where **ip_address** is the ip address of your LightwaveRF hub

To add Lightwave lights in the **light** section add:

```
light:
  - platform: lightwave
    no_registration: true
    devices:
      R1D1:
        name: Room one Device one
      R1D2:
        name: Room one Device two
      R8D3:
        name: Room eight Device three
   
```

To add Lightwave switches in the **switch** section add:

```
switch:
  - platform: lightwave
    no_registration: true
    devices:
      R1D1:
        name: Room one Device one
      R1D2:
        name: Room one Device two
      R8D3:
        name: Room eight Device three
   
```

Each **device** requires an **id** and a **name**. The **id** takes the form **R#D#** where **R#** is the room number 
and **D#** is the device number.
Without **no_registration** a switch or light will be created that when pressed will ask the hub to register. When pressed it will show a message on your WiFi Link asking you to pair the device. You have 12 seconds to push the button on the WiFi Link to accept this. Once done, you should be able to control your lights via Home Asssistant. Turning the switch or light off will deregister the link.
To hide the registration switch or light add **no_registration**.

### Acknowledgement
Thanks to Chirag Desai for paving the way to getting this component done.
