# Installation

[Zurück zur README](../README.md)

## Voraussetzungen

- Git
- Arduino IDE (Annahme: 1.8.x; die Firmware stammt aus der Marlin-1.0-Zeit und nutzt ältere Arduino-APIs)
- Arduino-Mega-kompatibles Board mit Motortreibern (Annahme; das tatsächliche Board muss in `Configuration.h` über `MOTHERBOARD` gewählt werden)
- Arduino-Bibliotheken je nach Konfiguration: `U8glib`, `LiquidCrystal_I2C`, `LiquidTWI2`; `Wire`, `SPI` und `LiquidCrystal` sind Teil der Arduino-Installation
- Für den mechanischen Aufbau: 3D-Drucker, Teile laut BOM (PDF)

## Schritt für Schritt

1. Repository klonen:
   ```bash
   git clone https://github.com/Infactionfreddy/Robot-ARM.git
   ```
2. Hardware nach BOM und Benutzerhandbuch aufbauen (`BCN3D-Moveo( STL und Code sowie Beschreibung )/BOM` und `USER MANUAL`). STL-Dateien liegen unter `STL files/`.
3. Pinout der Stepper-Treiber mit [EFB65ED7-3942-4A11-B39C-411EC5EF6D3A.jpeg](../EFB65ED7-3942-4A11-B39C-411EC5EF6D3A.jpeg) abgleichen.
4. In der Arduino IDE den Ordner `FIRMWARE/Marlin_BCN3D_Moveo/` öffnen.
5. Hinweis: Es liegen zwei inhaltsgleiche Dateien `Marlin.ino` und `Marlin_BCN3D_Moveo.ino` im Ordner. Falls beim Kompilieren Doppeldefinitionen oder Fehler auftreten, eine der beiden Dateien aus dem Sketch-Ordner entfernen (Annahme).
6. `Configuration.h` und `Configuration_adv.h` anpassen (siehe [KONFIGURATION.md](KONFIGURATION.md)).
7. Board und Port wählen, kompilieren und hochladen.
8. Verbindung per serieller Konsole testen, z. B. `M115` für den Firmware-Report (die Meldung ist in `language.h` definiert).

Die Alternative `Firmware/vscode_project/Firmware Robot ARM.zip` enthält ein VS-Code-Projekt (Inhalt nicht geprüft). Laut Autor ist es noch nicht für ein Board fertig angepasst.

## Update

```bash
git pull
```

Danach Konfiguration prüfen und die Firmware neu hochladen. Eigene Änderungen an `Configuration.h` vorher sichern. Gespeicherte EEPROM-Werte ggf. mit `M502`/`M500` zurücksetzen und speichern (Annahme, Marlin-Standard).

## Deinstallation

- Repository-Ordner löschen.
- Das Board mit einer anderen Firmware oder einem leeren Sketch überschreiben.
- Gegebenenfalls installierte Arduino-Bibliotheken über den Bibliotheksverwalter entfernen.
