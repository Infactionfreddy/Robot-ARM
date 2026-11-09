# Entwicklung

[Zurück zur README](../README.md)

## Lokale Entwicklungsumgebung

- Arduino IDE (Annahme: 1.8.x) oder `arduino-cli` mit AVR-Core, alternativ VS Code mit dem Projekt aus `Firmware/vscode_project/Firmware Robot ARM.zip` (ZIP muss zuerst entpackt werden; Inhalt nicht geprüft)
- Benötigte Bibliotheken je nach Schaltern installieren (`U8glib`, `LiquidCrystal_I2C`, `LiquidTWI2`)
- Zum Testen ein Board mit Motortreibern. Für reine Kompilier-Tests reicht ein ausgewähltes Board ohne angeschlossene Hardware.

## Code-Struktur

```text
FIRMWARE/Marlin_BCN3D_Moveo/
├── Marlin*.ino, Marlin_main.cpp, Marlin.h      # Einstieg und Hauptlogik
├── planner.*, stepper.*, motion_control.*      # Bewegung
├── temperature.*, thermistortables.h           # Temperatur
├── Configuration*.h, boards.h, pins.h          # Konfiguration
├── cardreader.*, Sd*.{cpp,h}                   # SD-Karte
├── ultralcd*.{cpp,h}, dogm_*, language_*.h     # Anzeige und Texte
└── Servo.*, watchdog.*, BlinkM.*, vector_3.*, qr_solve.*, digipot_mcp4451.cpp
```

Fast die gesamte Logik steckt in `.cpp`-Dateien. Die `.ino`-Dateien dienen laut Kommentar nur dazu, der Arduino IDE die benötigten Bibliotheken zu zeigen und GCode zu dokumentieren.

## Tests

Es gibt keine automatisierten Tests und keine CI-Konfiguration. Empfohlene manuelle Prüfung (Annahme):

1. Kompilieren mit verschiedenen Schalterkombinationen (laut Kommentar in `language.h`: mit und ohne `ULTIPANEL`/`ULTRALCD`/`SDSUPPORT`, alle Sprachen).
2. Serielle Verbindung testen (`M115`, `M119` für Endstop-Status).
3. Achsen zunächst ohne Last und mit niedriger Geschwindigkeit bewegen.

## Coding-Standards

- Der Code folgt dem Marlin-1.0-Stil: Präprozessor-Schalter (`#ifdef`), `FORCE_INLINE`, Texte in `language*.h`.
- Menütexte sind laut Kommentar auf 17 Zeichen begrenzt; Änderungen an Sprachdateien in allen Sprachen mitführen.
- Serielle Meldungen (`MSG_*` in `language.h`) nicht übersetzen.
- Lizenz-Header der übernommenen Dateien (GPL/LGPL) beibehalten.

## Bekannte Auffälligkeiten

- `Marlin.ino` und `Marlin_BCN3D_Moveo.ino` sind inhaltsgleich.
- `digipot_i2c_init()` in `digipot_mcp4451.cpp` iteriert mit `i<=` über die Array-Größe und liest dadurch ein Element zu viel (nur mit `DIGIPOT_I2C`).
- Das VS-Code-Projekt ist laut Autor noch nicht für ein Board fertig angepasst.

## Release-Ablauf

Es ist kein formaler Release-Prozess definiert (Annahme):

1. Änderungen auf einem Branch entwickeln und per Pull Request in `main` mergen.
2. Firmware kompilieren und, wenn möglich, am Arm testen.
3. Optional einen Git-Tag/GitHub-Release erstellen und die Konfigurationsdateien beilegen.
