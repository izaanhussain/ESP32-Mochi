# ESP32-Mochi
# ESP32 Mochi

A small animated desktop companion inspired by Dasai Mochi. this is using an ESP32-C3 SuperMini and a 0.96" SSD1306 OLED display. The project comes with a custom KiCad PCB, Gerber files and a very basic Arduino animation firmware that displays the bitmapped frames.

## Details

1) ESP32-C3 SuperMini as the controller
2) 0.96-inch, 128×64 SSD1306 I²C OLED
3) Bitmap-frame animation at a target of approximately 24 FPS
4) TTP223 touch sensor input
5) Buzzer connection
6) TP4056 USB-C LiPo charging module connection
7) Custom PCB designed in KiCad
8) KiCad source files and Gerber files included

## Required Library Setup

Open Arduino IDE
Install OLED libraries: Tools -> Manage Libraries -> search Adafruit SSD1306 -> install
fig1

Add esp32 additional board manager URL: Files -> Preferences -> add https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_dev_index.json to Additional Boards Manager URLs

install esp32 board manager: Tools -> Board -> Boards Manager -> search esp32 -> install esp32 by Espressif Systems

## Hardware

| Component | Quantity | Purpose |
|---|---:|---|
| ESP32-C3 SuperMini | 1 | Main controller |
| 0.96-inch SSD1306 I²C OLED, 128×64 | 1 | Animation display |
| TTP223 touch sensor module | 1 | Touch input |
| Buzzer | 1 | Sound output |
| TP4056 USB-C LiPo charger module | 1 | LiPo charging |
| 3.7 V single-cell LiPo battery | 1 | Portable power |
| Custom PCB | 1 | Connects the modules |
| 1×8 female socket headers, 2.54 mm pitch | 2 | ESP32-C3 module sockets |
| 1×4 female socket header, 2.54 mm pitch | 1 | OLED socket, if using a compatible module |
| Wires / solder | As needed | Battery and module connections |

See [`BOM.csv`](BOM.csv) for the parts list. Exact module dimensions and pin order can vary between suppliers; check your physical parts before assembly.

## Display

The project uses a:

**0.96" 128×64 SSD1306 I2C OLED**

The OLED is connected directly to the ESP32-C3.

## Pin connections

The firmware uses the following I²C pins on the ESP32-C3 SuperMini:

| Signal | ESP32-C3 pin |
|---|---|
| OLED SDA | GPIO8 |
| OLED SCL | GPIO9 |
| OLED power | 3V3 |
| OLED ground | GND |
| TTP223 output | GPIO3 |


### Power and charging

The TP4056's USB-C connector is the charging input when using a module with an onboard USB-C port. Connect the battery to the module's actual `B+` and `B−` terminals. If your module exposes `OUT+` and `OUT−`, verify the markings and protection circuit before using them as load outputs.


## Firmware

The Arduino firmware and bitmap frames are provided in [`Firmware/ESP32_Mochi.zip`](Firmware/ESP32_Mochi.zip).

## Firmware Installation 

1. Download the raw ESP32_Mochi.zip file
2. open Arduino IDE
3. open ESP32_Mochi.ino
4. upload to your device

### Requirements for uploading firmware

- Arduino IDE
- ESP32 Arduino core
- **Adafruit GFX Library**
- **Adafruit SSD1306**

### Upload

1. Extract `Firmware/ESP32_Mochi.zip`.
2. Open `ESP32_Mochi/ESP32_Mochi.ino`.
3. Keep `all_frames.h` alongside the sketch and retain the `frames/` folder if it is referenced by the extracted animation files.
4. Install the Adafruit GFX and Adafruit SSD1306 libraries through Library Manager.
5. Select the correct ESP32-C3 board and serial port.
6. Upload and open Serial Monitor at **115200 baud**.

The animation code targets 42 ms per frame (about 24 FPS). The actual frame rate depends on OLED refresh time and I²C performance.

## PCB files

The [`PCB/`](PCB/) folder contains the KiCad schematic, PCB layout, project settings, and a Gerber archive.

The [`Production/`](Production/) folder contains a copy of the Gerber archive for fabrication.

Before ordering:
1. Open the `.kicad_pcb` file in KiCad and inspect the front and back.
2. Open the Gerber archive in KiCad Gerber Viewer.
3. Confirm copper, solder mask, silkscreen, drill files, and `Edge.Cuts` outline are present.
4. Run DRC again after any design changes.
5. Check physical connector and module dimensions against your actual parts.

## Repository structure

```text
ESP32-Mochi/
├── Firmware/
│   └── ESP32_Mochi.zip
├── PCB/
│   ├── ESP32_Mochi.kicad_pro
│   ├── ESP32_Mochi.kicad_sch
│   ├── ESP32_Mochi.kicad_pcb
│   └── gerbers.zip
├── Production/
│   └── gerbers.zip
├── BOM.csv
├── LICENSE
└── README.md
```

## Credits

- Inspired by the Dasai Mochi concept.
- OLED animation uses the Adafruit GFX and Adafruit SSD1306 libraries.
- Designed by [Izaan Hussain](https://github.com/izaanhussain).

## License

This project is released under the MIT License. See [`LICENSE`](LICENSE).
