# Adafruit TinyUSB Core for Arduino

This repo is Arduino compatible variant from [TinyUSB stack](https://github.com/hathach/tinyusb) project to provide core USB functionality and CDC support for Arduino. Other class drivers such as Mass Storage, HID, MIDI etc ... are provided by [Adafruit_TinyUSB_Arduino](https://github.com/adafruit/Adafruit_TinyUSB_Arduino).

## Porting

Currently Arduino TinyUSB is used by following cores

- [Adafruit_nRF52_Arduino](https://github.com/adafruit/Adafruit_nRF52_Arduino)
- [Adafruit ArduinoCore-samd](https://github.com/adafruit/ArduinoCore-samd) **TinyUSB** must be selected in menu `Tools->USB Stack`

But it is also easy to port it to your own BSP as follows:

### Add the codes

Include this repo as submodule to your BPS cores folder e.g 

```
$ git submodule add https://github.com/adafruit/Adafruit_TinyUSB_ArduinoCore.git cores/arduino/TinyUSB/Adafruit_TinyUSB_ArduinoCore
```

Alternatively you could just copy the files over but will need to periodically sync to get the latest patches, features.

### Write the platform dependent codes

You will need to create 2 files 

- `tusb_config.h` for configuration that best suites your port and 
- `Adafruit_TinyUSB_port.cpp` to implement platform-dependent functions
  - **Adafruit_TinyUSB_Core_init()** to initialize USB hardware (clock, pullups) and tinyusb stack
  - **Adafruit_TinyUSB_Core_touch1200()** callback that fired when IDE use touch 1200 feature to put board into DFU mode
  - **Adafruit_USBD_Device** getSerialDescriptor(), detach(), attach()
