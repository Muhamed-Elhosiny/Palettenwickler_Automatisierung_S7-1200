# Palettenwickler_Automatisierung_S7-1200

Dieses Projekt ist eine Automatisierungslösung für eine **Palettenwickelmaschine** unter Verwendung einer **Siemens S7-1200 SPS**. 
Es umfasst die SPS-Programmierung, Motorsteuerung und Sensorintegration zur Automatisierung des Wickelprozesses.

# Projektübersicht

•	Die Wickelfolie mithilfe eines Motors auf- und abwärts zu bewegen.

•	Die Palette (Karton) während des Wickelvorgangs zu rotieren.

•	An den entsprechenden oberen und unteren Endschaltern zu stoppen.

•	Die Geschwindigkeit und Motorbewegungen über einen Frequenzumrichter (VFD) zu steuern.

The Box Wrapper is designed to:
- Move the wrapping film up and down using a motor.
- Rotate the box during wrapping.
- Stop at the appropriate top and bottom limits using limit switches.
- Control the speed and motor actions via a Variable Frequency Drive (VFD).


# Verwendete Komponenten:
1.	SPS: Siemens S7-1200
2.	Frequenzumrichter (VFD): 0,37 kW und 0,55 kW
3.	Sensoren:
   
    o	Oberer Endschalter (NO)
  	
    o	Unterer Endschalter (NO)
  	
    o	Näherungssensor zur Drehzahlzählung
  	
5.	Software: Codsys +TIA Portal mit Simulation in PLCSim



