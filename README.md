# yambms-chargeverter

## Summary

This allows an EG4 Chargeverter to query [YamBMS](https://github.com/Sleeper85/esphome-yambms) for SOC and Voltage.  YamBMS is designed to send your battery data to your inverter over CANbus, but an EG4 Chargeverter uses RS485.  The Chargeverter acts as the "server" which queries your batteries over RS485.  This emulates the EG4 battery protocol to allow YamBMS to respond to the Chargeverter queries as if it were an EG4 battery.

## WARNING
**USE THIS PROGRAM AT YOUR OWN RISK I ACCEPT NOI LIABILITY FOR ANY USE OF THIS PROGRAM.  THIS PROGRAM IS STRICTLY FOR REFERENCE ONLY!**

This is completely experimental.  While I have verified that this correctly sends SOC and Voltage data from YamBMS to the Chargeverter, the chargeverter expects 15 other data points that I have not verified.  Futhermore, the Anthropic Claude AI was used to guess at how this protocol should behave and what registers it should respond with.  It took a lot of trial and error just to get this working, do not trust it without extensive testing.


## Usage

Attach an RJ45 cable to the Chargeverter RJ45 like so:

- Pin 1 -> RS485 B
- Pin 2 -> RS485 A

Add the following to your YamBMS yaml file.  Be sure to change the rs485_uart_id and yambms_id appropriately:

```
  rs485_chargeverter:
    url: https://github.com/andrewfraley/yambms-chargeverter
    ref: main
    refresh: 0s
    files:
      - path: 'yambms_chargeverter_rs485.yaml'
        vars:
          rs485_uart_id: "uart_esp_3"
          yambms_id: "yambms1"
```

## Links
- [yambms-chargeverter](https://github.com/andrewfraley/yambms-chargeverter) (this repo)
- [YamBMS Github repo](https://github.com/Sleeper85/esphome-yambms)
- [YamBMS DIYSolarForum thread](https://diysolarforum.com/threads/yambms-jk-bms-can-with-new-cut-off-charging-logic-open-source.79325/)
