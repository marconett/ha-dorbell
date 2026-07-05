# 433 MHz Doorbell Receiver

Always-on, USB-powered receiver that turns a press of the 433 MHz doorbell sender (see `../sender`) into a `binary_sensor.doorbell` entity in Home Assistant.

## Parts

- **Waveshare ESP32-C6-Zero** (any ESP32-C6 devkit works)
- **RX480E-4**: 433 MHz receiver with built-in learning decoder
- 17.3 cm straight wire as antenna, soldered to the module's ANT pad
- Data-capable USB-C cable + USB power supply

## Wiring

| ESP32-C6 | RX480E-4 |
|---|---|
| 3V3 | VCC |
| GND | GND |
| GPIO1 | **D2** |

D0/D1/D3 stay unconnected. No other components needed.

> The learned code may land on a different D pin than D2 on other units: after pairing, check which output goes HIGH while the sender transmits and wire GPIO1 to that one.

## Pair the RX480E-4 to the sender (one-time)

Done entirely on the module, nothing to flash for this step:

1. Power the module.
2. Tap the on-board **learn button once** (LED lights), this selects momentary mode.
3. Press the doorbell. The LED blinks and turns off. Sender and receiver are now paired.
4. Press the doorbell again: the module LED should light for the duration of the press.

The pairing is stored in the module and survives power loss. To erase, hold the learn button ~8 s until the LED flashes.

## Flash the firmware

1. Install ESPHome
2. Create `secrets.yaml` next to `doorbell-receiver.yaml`:

   ```yaml
   wifi_ssid: "YourNetworkName"
   wifi_password: "YourWifiPassword"
   ```

3. Plug the board in via USB and run:

   ```sh
   esphome run receiver/doorbell-receiver.yaml
   ```

   Pick the correct serial port when asked. If no port shows up: swap in a data-capable cable, or enter download mode manually (hold **BOOT**, tap **RESET**, release BOOT, retry).

4. The command attaches to the log stream after flashing. Press the doorbell. The log should show the `Doorbell` sensor turning **ON**, then **OFF** ~1.5 s after release. Later updates work over Wi-Fi (OTA), no USB needed.

Alternatively, use ESPHome Device Builder to setup and flash the device.

## Connect to Home Assistant

Home Assistant auto-discovers the device: **Settings -> Devices & Services** -> the ESPHome card shows *doorbell-receiver* -> **Configure**. Trigger automations on `binary_sensor.doorbell` turning on.

## Enclosure

I provided a 3d printable enclosure in the form of .stl files.