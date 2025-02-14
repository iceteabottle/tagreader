# Tag Reader for Home Assistant

The tag reader is a simple to build/use NFC tag reader, specially created for [Home Assistant](https://www.home-assistant.io). It is using a D1 mini ESP 8266 and the PN532 NFC module. The firmware is built using [ESPhome](https://www.esphome.io).

I adopted the project from [adonno](https://github.com/adonno/), who created the original version of the [tag reader](https://github.com/adonno/tagreader). I added some features and fixed some bugs.

## Features

tbd

## Building the tag reader

To build your own tag reader, you need the following components:

 - ESP8266 D1 Mini
 - PN532 NFC Reader
 - WS2812 Neopixel LED
 - Buzzer
 - Some buttons

### Connecting the components

Also, make sure that you have set the switches on the PN532 to the following:
- Switch 1: On (up)
- Switch 2: Off (down)

This enables the PN532 module to communicate with the D1 over I2C, and is required for the modules to work together! The PN532 works on the 13.56Mhz (NTAG 213) Frequency. 

To flash the reader firmware to your D1 Mini you point ESPHome at [tagreader.yaml](tagreader.yaml).  

If you're new to ESPHome, we recommend that you use the [ESPHome Home Assistant add-on](https://esphome.io/guides/getting_started_hassio.html).

## Configuring for use with Home Assistant

If the tag reader is unable to connect to a wifi network, it will start a WiFi access point with a captive portal to allow you to enter your WiFi credentials.

The tag reader will be automatically discovered by Home Assistant once the tag reader is connected to the same network. You can follow the instructions in the UI to set it up.

I would strongly suggest to use secrets for the WiFi password and the Home Assistant API password. You can do this by adding the following to your `secrets.yaml` file:

```yaml
wifi_ssid: "Your WiFi SSID"
wifi_password: "Your WiFi password"
```

## Create a new music tag

To write a new music tag, you need to go to the developer tools in Home Assistant and call the service `write_music_tag` (look for something like `ESPHome: tagreader_419ac5_write_music_tag`). You need to provide the uri of the music file you want to write to the tag.

```yaml
music_url: spotify:album:xxx
```

## Import the blueprint

tbd

## Usage

Scanned tags can be managed from the tags interface in Home Assistant. You can find it under config -> tags.

## Troubleshooting

While adjusting adonnos code, I encountered some memory issues. It seems that the ESP8266 causes these issues. The ESP8266 isn't even recommended for use with ESPHome. To avoid these issues I moved almost the whole business logic from the ESP to Home Assistant. The ESP is now only responsible for reading the tags and sending the data almost directly to Home Assistant.

## ToDo

- [ ] Add feature description
- [ ] Add blueprint description
- [ ] Add images
- [ ] Update frizzing files
- [ ] Clean up firmware