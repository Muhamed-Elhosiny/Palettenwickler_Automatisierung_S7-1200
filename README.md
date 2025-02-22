## Palettenwickler_Automatisierung_S7-1200

Dieses Projekt ist eine Automatisierungslösung für eine **Palettenwickelmaschine** unter Verwendung einer **Siemens S7-1200 SPS**. 
Es umfasst die SPS-Programmierung, Motorsteuerung und Sensorintegration zur Automatisierung des Wickelprozesses.

<img width="626" alt="Plalletenwicker" src="https://github.com/user-attachments/assets/49109f56-0441-4153-a001-f891463261f7" />


## Projektübersicht 

Der Palettenwickler ist darauf ausgelegt:
  -	Die Wickelfolie mithilfe eines Motors auf- und abwärts zu bewegen.
  -	Die Palette (Karton) während des Wickelvorgangs zu rotieren.
  -	An den entsprechenden oberen und unteren Endschaltern zu stoppen.
  -	Die Geschwindigkeit und Motorbewegungen über einen Frequenzumrichter (VFD) zu steuern.

## Verwendete Komponenten:
1.	**SPS**: Siemens S7-1200
2.	**Frequenzumrichter (VFD)**: 0,37 kW und 0,55 kW
3.	**Sensoren**:
    -	Oberer Endschalter (NO)
    -	Unterer Endschalter (NO)
    -	Näherungssensor zur Drehzahlzählung
4.	**Software**: Codsys +TIA Portal mit Simulation in PLCSim

## Motorenbewertungen, Schutz und Verkabelung

### Auf/Ab-Motor
- **Leistung:** 0,37 kW
- **Spannung:** 380 V AC, 3-Phasen
- **Geschwindigkeitsregelung:** Erforderlich (Frequenzumrichter 0,37 kW)
- **Strom:** (I = W / (V x 0,7 x 1,73)) = 0,8 A
- **Überlastschutz:** Nicht erforderlich
- **Entfernung:** 1 m
- **Kabel:** 1 x 1,5 mm²

### Rotationsmotor
- **Leistung:** 0,55 kW
- **Spannung:** 380 V AC, 3-Phasen
- **Geschwindigkeitsregelung:** Erforderlich (Frequenzumrichter 0,55 kW)
- **Strom:** (I = W / (V x 0,7 x 1,73)) = 1,2 A
- **Überlastschutz:** Nicht erforderlich
- **Entfernung:** 1 m
- **Kabel:** 1 x 1,5 mm²

#### Gesamtleistungsaufnahme
- 0,37 kW + 0,55 kW = 0,92 kW

#### Kabelverlängerungen vom Motor zu den Klemmblöcken des Schaltschranks
- 6 Meter 1 x 1,5 mm²

# PLC-Auswahl:
## Digitale Ausgänge:
1.	Rotationsmotor
2.	Auf/Ab-Motor
3.	Auf/Ab-Motor
4.	Reserve 2
## Digitale Eingänge:
1.	Oberer Grenzschalter
2.	Unterer Grenzschalter
3.	Stretch-Näherungssensor
4.	Zähl-Näherungssensor
5.	Motor 1 Überlast
6.	Motor 2 Überlast
7.	Not-Aus
8.	Reserve 1
## Analoge Ausgänge:
  1.	VFD1 Frequenz
  2.	VFD2 Frequenz
# HMI-Auswahl:
Sie können ein HMI-Bildschirm wählen (die SPS sollte Profinet oder Modbus unterstützen)
Oder die Steuerung über einen Remote-PC (die SPS sollte einen Ethernet-Port haben)
Wir werden uns für die Remote-PC-basierte Steuerung entscheiden

## DC-Stromverbrauch und Stromversorgung
**Digitale Ausgänge**: 12 mA x 4 = 48 mA
**Digitale Eingänge**: 12 mA x 9 = 108 mA
**Analoge Ausgänge**: 12 mA x 2 = 24 mA
**Relais**:
•	PLC intern: 20 mA
•	VFD intern: 5 mA x 2 = 10 mA
**Gesamt**: 246 mA
Ein 1-Ampere-Netzteil wäre mehr als ausreichend.
Ein 1-Ampere-24-VDC-Industrienetzteil (mit Kurzschlussschutz) ist mehr als ausreichend.
## Auswahl der Leistungsschalter 
**Hauptleistungsschalter**
Gesamtleistungsaufnahme der Motoren = 0,92 kW = 920 W
PLC-E/A + PLC-interne Leistung + Relais beträgt kaum 5 W (zu gering)
**Gesamtleistung** = 920 W + 5 W + 20 % = 1,1 kW
**Gesamtstrom** = 1,1 kW / (380 V x 0,7 x 1,73) = 2,4 A

   
## Systemdiagramm
  -	Verdrahtungspläne:
    ![image](https://github.com/user-attachments/assets/c009bb51-13ee-4644-9caa-b8e45e068415)
   	<img width="281" alt="Page_2" src="https://github.com/user-attachments/assets/d6744e43-82f6-4ec4-80b6-f75ab117e2d9" />



## Wie es funktioniert
Der Wickelprozess ist vollständig automatisiert, mit:
  -	**Auf/Ab-Motor**, gesteuert durch die SPS.
  -	**Endschalter**, die den Motor stoppen, wenn der Wickelarm seine Grenzen erreicht.
  -	**Näheresensoren**, um die Wickelgeschwindigkeit und die Drehzahl zu überwachen.

### Logikimplementierung
Die SPS steuert das System mit Ladder-Logik und den folgenden Hauptfunktionen:
- **Motorkontrolle**: Der VFD steuert die Motoren, die durch SPS-Eingaben von den Sensoren gestartet und gestoppt werden.
- **Sicherheitsverriegelungen**: Endschalter verhindern eine Überdehnung des Wickelarms.

### Simulation und Test
- Das Projekt wurde zunächst im TIA Portal mit PLCSim simuliert, um eine ordnungsgemäße Motorsteuerung und Sensorkompatibilität sicherzustellen.
- (Fügen Sie Screenshots oder Code-Snippets Ihrer PLC-Simulationskonfiguration hinzu)

### Installation und Bereitstellung
1. Installieren Sie die Siemens S7-1200 SPS.
2. Verbinden Sie den VFD zur Steuerung der Motoren.
3. Verdrahten Sie die Endschalter und Sensoren an die SPS.
4. Laden Sie das SPS-Programm (im Ordner `/code`).
5. Überwachen und steuern Sie das System über HMI (optional).


### Zukünftige Verbesserungen
- Hinzufügen eines HMI für manuelle Steuerung und Überwachung.
- Verbesserung der Steuerung der Wickelmaterialspannung.

## Ordnerstruktur
- `/code`: Enthält die SPS-Programmierdateien (Ladder-Logik im TIA Portal-Format).
- `/docs`: Enthält alle Dokumentationen und Diagramme.
- `/simulations`: Dateien, die für die Simulationstests in PLCSim verwendet werden.

## Kontakt
Wenn Sie Fragen zu diesem Projekt haben, können Sie mich gerne unter

[Muhamad.Elhosiny@example.com] kontaktieren.


