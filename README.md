# ESP32 Mochi

A small animated desktop companion inspired by Dasai Mochi. this is made by using an ESP32-C3 SuperMini and a 0.96" SSD1306 OLED display. The repo has a custom KiCad PCB, Gerber files and a very basic Arduino animation firmware that displays the bitmapped frames of the 712 GIFs.

<img width="980" height="580" alt="image" src="https://github.com/user-attachments/assets/d95bfdc8-c6dd-47f5-9f71-5e69a23b7073" />


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

you can see the [`BOM.csv`](BOM.csv) for the list of parts.

## Display

The project uses a:

**0.96" 128×64 SSD1306 I2C OLED**

The OLED is connected directly to the ESP32-C3.

## Pin connections

The firmware uses the I²C pins given below on the ESP32-C3 SuperMini:-

| Signal | ESP32-C3 pin |
|---|---|
| OLED SDA | GPIO8 |
| OLED SCL | GPIO9 |
| OLED power | 3V3 |
| OLED ground | GND |
| TTP223 output | GPIO3 |


### About Power and charging

The USB-C connector on this TP4056 serves as the charging input. The battery should be connected to the actual B+ and B− pins on the module. If your module has OUT+ and OUT− pins, ensure that they are correctly labelled and protected before using them as load outputs.


## Firmware

The Arduino firmware and bitmap frames are provided in [`Firmware/ESP32_Mochi.zip`](Firmware/ESP32_Mochi.zip).

## Firmware Installation 

1. Download the raw ESP32_Mochi.zip file
2. open Arduino IDE
3. open ESP32_Mochi.ino
4. upload to your device

### Requirements for uploading firmware

1) Arduino IDE
2) ESP32 Arduino core
3) **Adafruit GFX Library**
4) **Adafruit SSD1306**

### Upload

1. extract Firmware/ESP32_Mochi.zip
2. open the ESP32_Mochi/ESP32_Mochi.ino file
3. ensure that all_frames.h is in the same directory as the sketch
4. install the Adafruit GFX and Adafruit SSD1306 libraries using Library Manager
5. select the correct ESP32-C3 board and serial port
6. upload the sketch and open the Serial Monitor (with baud rate 115200)

The current firmware targets 42 ms per frame (means about 24 FPS).

## PCB

The [`PCB/`](PCB/) folder contains the KiCad schematic, PCB layout, project settings, and a Gerber files zip.

The [`Production/`](Production/) folder contains a copy of the Gerber files for fabrication.

<img width="961" height="591" alt="image" src="https://github.com/user-attachments/assets/de5a71df-b01e-4675-bbd0-179ed10dd1cd" />

<img width="951" height="581" alt="image" src="https://github.com/user-attachments/assets/dda3b965-639a-45d8-91fa-da975e654d29" />

<img width="496" height="326" alt="image" src="https://github.com/user-attachments/assets/7750ec52-decf-45af-84c2-f72194fd31dc" />

<img width="393" height="282" alt="image" src="https://github.com/user-attachments/assets/484dfc6f-9038-4114-afed-66bea2e9c80b" />



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

## License

This project is released under the MIT License. See [`LICENSE`](LICENSE).
