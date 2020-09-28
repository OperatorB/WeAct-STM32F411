# Getting started with PlatformIO and arduino framework on Windos.
<div align="left"><img alt="WeAct STM32F411" src="https://docs.zephyrproject.org/latest/_images/blackpill-v2.jpg" width="300px"/></div>

## Steps:

- 'Update driver' of STM device with Windows Device Manager
- install Zadig software
- connect USB and put STM32F411 to bootloader mode (hold down Boot0 while pressing NRST). In Windows Device Manager you should see 'STM Device in DFU mode'.

![Update driver](/before.png)

- use Zadig to switch driver (select 'STM32 BOOTLOADER' then click 'Replace Driver'). After all you should see 'STM32 BOOTLOADER' listed in Device Manager.

![Zadig](/zadig.png)
![After](/after.png)

- browse into your .platformio/packages/tool-stm32duino and replace 'dfu-util' with V0.9 (I have tested only V0.9)
- in PlatformIO .ini file specify :

```
[env:blackpill_f411ce]
platform = ststm32
board = blackpill_f411ce
framework = arduino
board_build.mcu = stm32f411ceu6
board_build.f_cpu = 100000000L
upload_protocol = dfu
build_flags =
  -D PIO_FRAMEWORK_ARDUINO_ENABLE_CDC
  -D USBCON
  -D USB_VID=0x0483
  -D USB_MANUFACTURER="Unknown"
  -D USB_PRODUCT=""BLACKPILL_411CE""
  -D HAL_PCD_MODULE_ENABLED`
```

- write, compile and upload your favourite code (e.g. blink)
- Practice, push your limits and contribute to some awesome projects!
##
<H3>:warning:Unfortunately, you should use the Boot0 and NRST buttons on each upload. Fortunately, you can do it with one hand after some practice.


Sources used:
```
-https://www.hanselman.com/blog/HowToFixDfuutilSTMWinUSBZadigBootloadersAndOtherFirmwareFlashingIssuesOnWindows.aspx
-https://github.com/stm32duino/Arduino_Core_STM32/issues/876
-za internet
```


