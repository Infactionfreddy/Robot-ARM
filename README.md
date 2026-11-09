# Robot-ARM

Umsetzung eines 3D-gedruckten Roboterarms auf Basis des BCN3D Moveo, inklusive Marlin-basierter Arduino-Firmware (C++), CAD-/STL-Dateien und Handbüchern.

![C++](https://img.shields.io/badge/Sprache-C%2B%2B-00599C?logo=cplusplus&logoColor=white)
![Arduino](https://img.shields.io/badge/Plattform-Arduino%20(AVR)-00979D?logo=arduino&logoColor=white)

> Hinweis des Autors: Hier gibt es vielleicht eine Version des Roboterarms in einer Beta-Version. Das Firmware-Projekt in `Firmware/vscode_project` passt noch nicht zu 100 % zu einem der Boards.

## Features

- Vollständiger Bausatz des BCN3D Moveo: CAD-Dateien (SolidWorks), STL-Dateien für den 3D-Druck, Stückliste (BOM) und Benutzerhandbuch (PDF)
- Marlin-Firmware (Sprinter/Grbl-Mashup) für den Moveo mit Stepper-Ansteuerung, Bewegungsplaner und G-Code über die serielle Schnittstelle
- Optionale Unterstützung für SD-Karte, LCD-Display (HD44780 und ST7920), EEPROM-Einstellungen, Watchdog, Servo und Bett-Nivellierung (abhängig von der Konfiguration)
- Mehrsprachige Menütexte (u. a. Deutsch, Englisch, Spanisch, Französisch)
- Stepper-Driver-Pinout als Bild im Repository

## Tech-Stack

- C/C++ (Arduino/AVR, avr-gcc), Arduino IDE oder Arduino-Toolchain
- Marlin 1.0.x (Sprinter + Grbl), SdFat, U8glib, LiquidCrystal
- SolidWorks (CAD), STL (3D-Druck)

## Schnellstart

### Voraussetzungen

- Arduino IDE (Annahme: 1.8.x) und ein Arduino-Mega-kompatibles Board mit passender Motorelektronik (z. B. RAMPS; Annahme, siehe Konfiguration)
- Zusätzliche Arduino-Bibliotheken je nach Konfiguration, z. B. `U8glib`, `LiquidCrystal_I2C`, `LiquidTWI2`
- USB-Kabel

### Installation

```bash
git clone https://github.com/Infactionfreddy/Robot-ARM.git
cd Robot-ARM
```

### Start (Firmware flashen)

1. `BCN3D-Moveo( STL und Code sowie Beschreibung )/FIRMWARE/Marlin_BCN3D_Moveo/` in der Arduino IDE öffnen.
2. `Configuration.h` prüfen und anpassen (Board, Pins, Schritte pro mm, Endstops).
3. Board und Port wählen, Sketch hochladen.
4. Per serieller Konsole (Baudrate laut `Configuration.h`) G-Code senden.

Details: [docs/INSTALLATION.md](docs/INSTALLATION.md)

## Konfiguration

Es gibt keine Umgebungsvariablen. Die Firmware wird zur Compile-Zeit über `#define`-Schalter konfiguriert:

| Einstellung | Datei | Zweck |
|---|---|---|
| `MOTHERBOARD` | Configuration.h | Zielboard (siehe `boards.h`) |
| `SDSUPPORT` | Configuration.h | SD-Karten-Unterstützung |
| `ULTRA_LCD` / `ULTIPANEL` | Configuration.h | LCD und Bedienpanel |
| `EEPROM_SETTINGS` | Configuration.h | Einstellungen im EEPROM speichern |
| `LANGUAGE_INCLUDE` | language.h | Sprache der Menütexte |
| `USE_WATCHDOG` | Configuration.h / Configuration_adv.h | Watchdog-Reset |

Alle Optionen: [docs/KONFIGURATION.md](docs/KONFIGURATION.md)

## Projektstruktur

```text
.
├── README.md
├── EFB65ED7-3942-4A11-B39C-411EC5EF6D3A.jpeg   # Stepper-Driver-Pinout
├── Firmware/
│   └── vscode_project/                        # Firmware als ZIP + Hinweis
├── BCN3D-Moveo( STL und Code sowie Beschreibung )/
│   ├── BOM/                                   # Stückliste (PDF)
│   ├── CAD files/                             # SolidWorks-Dateien
│   ├── FIRMWARE/Marlin_BCN3D_Moveo/           # Marlin-Firmware (C++/Arduino)
│   ├── STL files/                             # Druckdateien je Gelenk
│   ├── USER MANUAL/                           # Benutzerhandbuch (PDF)
│   ├── LICENSE
│   └── README.md                              # Original-README von BCN3D
└── docs/                                      # Detaildokumentation
```

## Pinout

Stepper-Driver-Pinout: [EFB65ED7-3942-4A11-B39C-411EC5EF6D3A.jpeg](EFB65ED7-3942-4A11-B39C-411EC5EF6D3A.jpeg)

## Dokumentation

- [Architektur](docs/ARCHITEKTUR.md)
- [Installation](docs/INSTALLATION.md)
- [Konfiguration](docs/KONFIGURATION.md)
- [Entwicklung](docs/ENTWICKLUNG.md)

## Links und Danksagung

- [BCN3D Moveo (Original)](https://github.com/BCN3D/BCN3D-Moveo)
- [Firmware Marlin BCN3D-Moveo](https://github.com/BCN3D/BCN3D-Moveo/tree/master/FIRMWARE/Marlin_BCN3D_Moveo)
- [Robot Arm Designer (Design für die neueste Version)](https://github.com/4ndreas?tab=repositories)

Das Projekt basiert auf einem Projekt von [Andreas Hölldorfer](http://chaozlabs.blogspot.de/) ([Hackaday.io](https://hackaday.io/project/3800-3d-printable-robot-arm), [Github](https://github.com/4ndreas/BetaBots-Robot-Arm-Project/tree/master), [Youtube](https://www.youtube.com/channel/UCeFKz1UJUd5YuxS1ZikqYwA)). Der BCN3D Moveo wurde von BCN3D Technologies in Zusammenarbeit mit dem Departament d'Ensenyament der Generalitat de Catalunya entwickelt.

## Lizenz

Im Unterordner `BCN3D-Moveo( STL und Code sowie Beschreibung )/` liegt eine [LICENSE](<BCN3D-Moveo( STL und Code sowie Beschreibung )/LICENSE>)-Datei. Die Marlin-/Grbl-/SdFat-Quellen tragen GPL-v3-Header, einzelne Bibliotheken LGPL 2.1. Eine LICENSE im Repository-Root existiert nicht.
