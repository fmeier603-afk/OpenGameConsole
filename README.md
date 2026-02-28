# OpenGameConsole
Open source non profit game console with modularity and a linux like design

# Modulare Silent‑Konsole — Vollständige Technische Dokumentation (README)

Eine offene, modulare, extrem leise Wohnzimmer‑Konsole mit Retro‑ und Steam‑Modus, Matter‑Smart‑Home‑Integration, eigenem Slot‑Display‑System, 3‑Wege‑Modusschalter, 180‑mm‑Silent‑Kühlung und einem markanten gelb‑pinken Design. Dieses Dokument beschreibt die gesamte Architektur, Mechanik, Elektronik, Software‑Logik und UX‑Philosophie.

---

# 1. Systemübersicht

Die Konsole ist ein hybrides Gerät zwischen:
- Gaming‑Konsole  
- Mini‑PC  
- Smart‑Home‑Gerät  
- Modularer Plattform  

Zentrale Eigenschaften:
- Vier modulare Hardware‑Slots  
- Mini‑LCD‑Displays pro Slot  
- Silent‑Kühlung über 180‑mm‑Radiatorlüfter  
- Mechanischer 3‑Wege‑Modusschalter mit Druckfunktion  
- Matter‑Integration (Alexa‑fähig)  
- Retro‑Modus + Steam‑Modus  
- Organisches Mesh‑Gitter mit Logo‑Schlitzen  
- Vollständig offline nutzbar  
- Offen, modding‑freundlich, auditierbar  

---

# 2. Hardware‑Architektur

## 2.1 Gehäuse & Mechanik
- Material: Aluminium + ABS‑Kunststoff  
- Farbe: Gelb (Gehäuse), Neon‑Pink (Akzente, Displays, UI‑Elemente)  
- Formfaktor: Kompakter NAS‑ähnlicher Tower  
- Vier Gummistandfüße:
  - Vibrationsdämpfung  
  - Abstand für Airflow  
  - Rutschfestigkeit  

## 2.2 Unterseite & Mesh‑Gitter
- Großes Mesh‑Gitter über dem 180‑mm‑Lüfter  
- Organische Firmenlogo‑Schlitze (Logo folgt später)  
- Offene Fläche: 40–55 %  
- Ziel:
  - Hoher Airflow  
  - Minimale Turbulenzen  
  - Akustisch weicher Luftstrom  
  - Markenidentität sichtbar  

## 2.3 Kühlung
- 180‑mm Radiatorlüfter (Bottom‑Intake)  
- Luftstromrichtung: Unten → Oben  
- Vorteile:
  - Sehr niedrige Drehzahlen  
  - Gleichmäßige Kühlung aller Module  
  - Positiver Druck → weniger Staub  
  - Keine Hotspots  

### Lüfter‑Drehzahlen
- Idle: 300–400 RPM  
- Gaming: 600–800 RPM  
- Maximal: 900–1000 RPM  

### Thermische Zonen
- Zone A: APU / CPU  
- Zone B: GPU‑Modul (z. B. GT 710)  
- Zone C: Modul‑Backplane  
- Zone D: Netzteil / IO  

---

# 3. Modul‑System

## 3.1 Slots
- Vier modulare Bays  
- Hot‑Swap‑fähig  
- Mechanische Führungsschienen  
- Elektrische Verbindung:
  - PCIe (x1–x4 je nach Modul)  
  - GPIO‑Sidechannel für Status & Zertifizierung  

## 3.2 Modul‑Erkennung
- Jedes Modul meldet:
  - Seriennummer  
  - Hersteller  
  - Firmwareversion  
  - Zertifizierungsstatus  

## 3.3 Zertifizierung
- **Zertifiziert:**  
  - Offiziell unterstützte Module  
  - Volle Funktionalität  

- **Nicht zertifiziert / Fake:**  
  - Funktion erlaubt  
  - Markierung im UI  
  - Warnsymbol am Slot‑Display  

---

# 4. Slot‑Displays (Mini‑LCDs)

## 4.1 Hardware
- Größe: 5×5 mm  
- Typ: OLED oder monochromes LCD  
- Ansteuerung: I²C oder SPI  
- Controller: MCU‑Hub (z. B. STM32C0 oder RP2040)  

## 4.2 Funktionen
- Slot‑Nummer  
- Modul‑Icon  
- Zertifizierungsstatus  
- Warnsymbol  
- Boot‑Logo  
- Animationen  
- Personalisierbare Themes  

## 4.3 Verhalten
- **Immer an**, außer im Spielbetrieb  
- Im Spielbetrieb → Displays **aus**  
- Beim Boot → Firmenlogo auf allen Displays  
- Bei Modulwechsel → kurze Animation  
- Bei Fake‑Modul → blinkendes Warnsymbol  

---

# 5. Warnsystem

## 5.1 Software‑Overlay
- Warndreieck oben rechts/links  
- Zeigt Slot‑Nummer (z. B. „⚠️ S3“)  
- Klick → Info‑Panel  

## 5.2 Info‑Panel
- Slot‑Nummer  
- Modulname  
- Zertifizierungsstatus  
- Seriennummer  
- Firmwareversion  
- Risiko‑Hinweis  
- Option: Warnsymbol deaktivieren  

## 5.3 Hardware‑Warnung
- Slot‑Display blinkt  
- Farbe/Animation konfigurierbar  

---

# 6. Modus‑Schalter (Power + 3‑Wege‑Slider)

## 6.1 Mechanik
- Kombinierter Druckknopf + Schiebeschalter  
- Druck = Ein/Aus  
- Schiebefunktion = 3 Positionen  

## 6.2 Werkseinstellungen
- Links: Retro‑Modus  
- Mitte: Steam‑Modus  
- Rechts: Utility‑Modus  

## 6.3 Software‑Flexibilität
- Später frei belegbar  
- Pro Benutzerprofil konfigurierbar  
- Kann Smart‑Home‑Aktionen auslösen  

## 6.4 Elektrische Signale
- MODE = 0/1/2  
- POWER = Momentary‑Kontakt  
- MCU liest MODE beim Boot aus  

---

# 7. Software‑Modi

## 7.1 Retro‑Modus
- EmulationStation  
- Minimalistisches UI  
- Schnelle Bootzeiten  
- Slot‑Displays aktiv  

## 7.2 Steam‑Modus
- Steam‑OS  
- PC‑Gaming  
- Slot‑Displays im Spielbetrieb deaktiviert  

## 7.3 Utility‑Modus
- BIOS  
- Recovery  
- Smart‑Home‑Setup  
- Modul‑Diagnose  

---

# 8. Smart‑Home‑Integration

## 8.1 Matter‑Integration
- Konsole tritt als **Matter‑Gerät** auf  
- Lokale Steuerung  
- Keine Cloud‑Pflicht  
- Kompatibel mit:
  - Alexa  
  - Google Home  
  - Apple Home  

## 8.2 Beispielbefehle
- „Alexa, update das Spiel auf Slot 2.“  
- „Alexa, starte die Konsole im Retro‑Modus.“  
- „Alexa, schalte die Konsole aus.“  

## 8.3 Automationen
- Beim Einschalten → Licht dimmen  
- Beim Start eines Spiels → TV auf HDMI 1  
- Beim Update → LED‑Strip pulsiert pink  

---

# 9. Netzwerk & Funk

## 9.1 Wi‑Fi 7 (802.11be)
- Sehr hohe Bandbreite  
- Niedrige Latenz  
- Multi‑Link‑Operation  
- Perfekt für Steam‑Downloads  

## 9.2 Bluetooth 5.4–6.0
- Controller  
- Headsets  
- LE Audio  
- Low‑Power‑Sensoren  

---

# 10. Boot‑Sequenz (Detail)

1. **Power‑Button gedrückt**  
2. MCU aktiviert Slot‑Displays → Firmenlogo  
3. MCU liest Schalterposition (MODE 0/1/2)  
4. Boot‑Flag wird gesetzt  
5. BIOS/UEFI startet  
6. OS‑Loader wählt Modus basierend auf Boot‑Flag  
7. Slot‑Displays wechseln in Statusmodus  
8. UI lädt  
9. Bei Spielstart → Displays aus  

---

# 11. Elektronik‑Architektur

## 11.1 MCU‑Hub
- Verbindet:
  - Slot‑Displays  
  - Modul‑Sidechannel  
  - Modus‑Schalter  
  - Warnsystem  
- Aufgaben:
  - Boot‑Flag setzen  
  - Display‑Steuerung  
  - Modul‑Status auslesen  
  - Smart‑Home‑Trigger  

## 11.2 Backplane
- PCIe‑Verteilung  
- GPIO‑Sidechannel  
- Hot‑Swap‑Erkennung  
- Power‑Management  

## 11.3 Power‑Management
- Soft‑On über MCU  
- Hard‑Off über Long‑Press  
- Modul‑Power‑Gating  

---

# 12. Design‑Philosophie

- Modular  
- Offen  
- Silent  
- Visuell ikonisch  
- Smart‑Home‑fähig  
- Retro‑freundlich  
- Zukunftssicher  
- Mechanisch spürbar  
- Softwareseitig flexibel  

---

# 13. Erweiterungspotenzial

- Eigene Smart‑Home‑Module:
  - Ambient‑Light  
  - IR‑Blaster  
  - Sensor‑Module  
  - Thread‑Border‑Router  
- Erweiterte Boot‑Animationen  
- Freie Schalterbelegung  
- Logo‑Design für Mesh & Displays  
- Erweiterte Matter‑Funktionen  
- Modul‑Marktplatz  

---

# 14. Projektstatus

- Name: Wird später definiert  
- Logo: Wird später definiert  
- Status: Konzeptphase / Dokumentation
