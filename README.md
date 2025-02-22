## Palettenwickler_Automatisierung_S7-1200

Dieses Projekt ist eine Automatisierungslösung für eine **Palettenwickelmaschine** unter Verwendung einer **Siemens S7-1200 SPS**. 
Es umfasst die SPS-Programmierung, Motorsteuerung und Sensorintegration zur Automatisierung des Wickelprozesses.
xx

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
  -	Verdrahtungspläne: xx

## Wie es funktioniert
Der Wickelprozess ist vollständig automatisiert, mit:
  -	**Auf/Ab-Motor**, gesteuert durch die SPS.
  -	**Endschalter**, die den Motor stoppen, wenn der Wickelarm seine Grenzen erreicht.
  -	**Näheresensoren**, um die Wickelgeschwindigkeit und die Drehzahl zu überwachen.

 ### Logic Implementation
The PLC controls the system using ladder logic with the following key functions:
- **Motor Control**: The VFD drives the motors, which are started and stopped by PLC inputs from the sensors.
- **Safety Interlocks**: Limit switches prevent over-extension of the wrapping arm.

### Simulation and Testing
- The project was first simulated in TIA Portal using PLCSim to ensure proper motor control and sensor integration.
- (Include screenshots or code snippets of your PLC simulation setup)

### Installation and Deployment
1. Install the Siemens S7-1200 PLC.
2. Connect the VFD to control the motors.
3. Wire the limit switches and sensors to the PLC.
4. Download the PLC program (located in the `/code` folder).
5. Monitor and control the system via HMI (optional).

### Future Improvements
- Adding an HMI for manual control and monitoring.
- Improving the wrapping material tension control.

## Folder Structure
- `/code`: Contains the PLC programming files (Ladder Logic in TIA Portal format).
- `/docs`: Contains all the documentation and diagrams.
- `/simulations`: Files used for simulation testing in PLCSim.

## Contact
If you have any questions about this project, feel free to contact me at 

[Muhamad.Elhosiny@example.com]
   




