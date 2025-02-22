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
**Digitale Ausgänge:** 12 mA x 4 = 48 mA  
**Digitale Eingänge:** 12 mA x 9 = 108 mA  
**Analoge Ausgänge:** 12 mA x 2 = 24 mA  
**Relais:**  
• **PLC intern:** 20 mA  
• **VFD intern:** 5 mA x 2 = 10 mA  
**Gesamt:** 246 mA  

Ein **1-Ampere-Netzteil** wäre mehr als ausreichend.  
Ein **1-Ampere-24-VDC-Industrienetzteil** (mit Kurzschlussschutz) ist mehr als ausreichend.  

## Auswahl der Leistungsschalter
### Hauptleistungsschalter
**Gesamtleistungsaufnahme der Motoren** = 0,92 kW = 920 W  
**PLC-E/A + PLC-interne Leistung + Relais** beträgt kaum 5 W (zu gering)  
**Gesamtleistung** = 920 W + 5 W + 20 % = **1,1 kW**  
**Gesamtstrom** = 1,1 kW / (380 V × 0,7 × 1,73) = **2,4 A**

## Hauptleistungsschalter

### Gesamtstrom = 1,1 kW / (380 × 0,7 × 1,73) = **2,4A**

**Hinweis:** Ein Hauptleistungsschalter dient hauptsächlich zum Schutz des Eingangsstromkabels.

### Auswahl des Hauptleistungsschalters:
1. **Überprüfen Sie die benötigte Kabellänge** zwischen der Hauptstromquelle (Transformator, Stromverteilungstafel) und Ihrem Hauptleistungsschalter.  
   _Angenommen, unser Fall beträgt **10m**._

2. **Gesamten Stromverbrauch des Schaltschrankes berechnen:**  
   _Unser Fall: **2,4 × 10** (unter Berücksichtigung von Einschaltströmen) = **24A**_

3. **Für den Hauptleistungsschalter sollte mindestens ein 1,5mm²-Kabel verwendet werden**, insbesondere für Schaltschränke mit Motorlasten.  
   Aber reicht das hier aus? Ist der Spannungsabfall **weniger als 3%**?

4. **Spannungsabfall berechnen:**  
   **Spannungsabfall (%) = (1,73 × Strom × Kabelimpedanz pro Meter × Kabellänge × 100) / Spannungsquelle**  

   _Unser Fall:_  
   **(1,73 × 24 × 0,0138 × 10 × 100) / 380 = 1,5%** _(weniger als 3%, akzeptabel!)_

5. **Maximalstrom für 1,5mm²-Kabel gemäß Tabelle:**  
   _Es beträgt **25A**._

   Daher sollte unser Haupt-MCB bei **25A Typ C** liegen _(zur Berücksichtigung von Einschaltströmen)_.

## MCBs:

1. **24VDC-Stromversorgung**: MCB von **1A** - **1-poliger MCB**  
   _Schalten_
2. **PLC**: **1A Steuerstromkreis** - MCB **1A** - **1-poliger MCB**  
   _Schalten_
3. **VFD 0,55 kW**: **0,55 kW** / (380 × 1,73 × 0,7) = **1,2A**  
   **2A 3-poliger MCB** - **Typ C (5–10-fach)**  
   _Schalten_
4. **VFD 0,37 kW**: **0,37 kW** / (380 × 1,73 × 0,7) = **0,8A**  
   **1A 3-poliger MCB** - **Typ C (5–10-fach)**  
   _Schalten_

---

**Da diese MCBs nur zum Schalten verwendet werden,**  
**ist jede MCB-Bewertung höher als die maximale Gerätebewertung ausreichend.**
## Sicherungen:
Da unser gesamter Stromverbrauch etwa **250mA** beträgt,  
wäre eine **500mA**-Sicherung geeignet (**nächsthöherer Sicherungsstandard**).

# Schematic Design

### Überlastschutz

   ![image](https://github.com/user-attachments/assets/fd148ef4-1e95-44df-a96b-4d85cdf3e311)

### Motoren

  ![image](https://github.com/user-attachments/assets/2af1b5b4-ab75-4734-b485-80b5f2e23c30)


### Steurung

  ![image](https://github.com/user-attachments/assets/4bdc621a-7201-4847-91b6-36f2fac67bc1)

###Sensoren

  ![image](https://github.com/user-attachments/assets/ebae550c-7cd4-4fd9-931f-47372208eb0f)




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


