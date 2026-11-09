# Konfiguration

[Zurück zur README](../README.md)

## Umgebungsvariablen

Das Projekt verwendet keine Umgebungsvariablen. Die Firmware wird zur Compile-Zeit über Präprozessor-Schalter konfiguriert. Die konkreten Werte in `Configuration.h` und `Configuration_adv.h` wurden nicht ausgewertet; die Tabellen beschreiben die im Code sichtbaren Schalter.

## Konfigurationsdateien

| Datei | Inhalt |
|---|---|
| `Configuration.h` | Hauptkonfiguration (Board, Motoren, Temperatur, LCD, SD) |
| `Configuration_adv.h` | Erweiterte Optionen (z. B. Digipot-Ströme, Watchdog) |
| `boards.h` | Liste unterstützter Boards (`BOARD_*`), Makro `MB(board)` |
| `pins.h` | Pinbelegung je Board |
| `language.h` / `language_*.h` | Sprache der Menütexte |
| `SdFatConfig.h` | SD-Bibliothek |

## Wichtige Schalter

| Schalter | Wirkung |
|---|---|
| `MOTHERBOARD` | Zielboard, z. B. `BOARD_RAMPS_13_EFB` (33) |
| `SERIAL_PORT` | Serieller Port (Standard 0, falls nicht definiert) |
| `EXTRUDERS` | Anzahl Extruder-Achsen (max. 3) |
| `BLOCK_BUFFER_SIZE` | Größe des Planer-Puffers |
| `MM_PER_ARC_SEGMENT`, `N_ARC_CORRECTION` | Genauigkeit der Bogenbewegung |
| `SDSUPPORT` | SD-Karte aktivieren |
| `SDCARDDETECT`, `SDCARDDETECTINVERTED` | Kartenerkennungs-Pin und Polarität |
| `ULTRA_LCD`, `ULTIPANEL`, `NEWPANEL` | LCD und Bedienpanel |
| `DOGLCD`, `U8GLIB_ST7920` | Grafisches Display |
| `REPRAPWORLD_KEYPAD` | Zusätzliches Keypad |
| `EEPROM_SETTINGS` | Einstellungen im EEPROM |
| `DISABLE_M503` | Ausgabe der Einstellungen abschalten |
| `USE_WATCHDOG`, `WATCHDOG_RESET_MANUAL` | Watchdog (4-s-Timeout) |
| `ENABLE_AUTO_BED_LEVELING`, `AUTO_BED_LEVELING_GRID` | Bett-Nivellierung (vector_3, qr_solve) |
| `DIGIPOT_I2C`, `DIGIPOT_I2C_MOTOR_CURRENTS` | I2C-Digipot (MCP4451) für Motorströme |
| `BLINKM` | BlinkM-LED über I2C |
| `PIDTEMP`, `PIDTEMPBED` | PID-Temperaturregelung |
| `THERMAL_RUNAWAY_PROTECTION_PERIOD` | Schutz gegen Thermal Runaway |
| `BABYSTEPPING` | Feinjustierung während der Bewegung |
| `AUTOTEMP`, `ADVANCE`, `FILAMENT_SENSOR` | Weitere Extruder-Funktionen |
| `CUSTOM_MENDEL_NAME`, `MACHINE_UUID` | Name und UUID im M115-Report |

## Sprache

In `language.h` wird über `LANGUAGE_INCLUDE` eine der Dateien `language_<kürzel>.h` eingebunden. Standard ist `en`. Verfügbar: en, de, pl, fr, es, ru, it, pt, fi, an, nl, ca, eu. Beispiel:

```cpp
#define LANGUAGE_INCLUDE GENERATE_LANGUAGE_INCLUDE(de)
```

## Hooks/Filter

Es gibt keine Hooks oder Filter. Änderungen erfolgen direkt im Quellcode oder über die Schalter oben.

## Hinweis zu Pins

Das Pinout der Stepper-Treiber ist als Bild beigelegt: [EFB65ED7-3942-4A11-B39C-411EC5EF6D3A.jpeg](../EFB65ED7-3942-4A11-B39C-411EC5EF6D3A.jpeg). Die Pins müssen zum gewählten `MOTHERBOARD` und zur Verdrahtung passen.
