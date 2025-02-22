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
   
## Systemdiagramm
  -	Verdrahtungspläne:
    ![image](https://github.com/user-attachments/assets/c009bb51-13ee-4644-9caa-b8e45e068415)


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


