# 5-DOF-Roboterarm-mit-Schraubdreher
Ein Roboterarm mit 5 Freiheitsgraden 5-DOF umfasst mechanisches Design (Solidworks v2018), Regelungstechnik und Codegenierung für ROS oder Hardware ( Matlab Simulink Simscape 3D-Body Toolbox)

# Design & Modellierung

Mechanisches Design : erstellt in Solidworks.
Simulationsmodell : aufgebaut in Simulink / Simscape Multibody.
Aufbau eines Rigid Body Tree zur Darsstellung der Roboterstruktur.

<img width="629" height="502" alt="gfnf" src="https://github.com/user-attachments/assets/2783abcc-95df-4baf-815a-452410724a50" />


# Wichtige Simulink Blöke 

ph-s (Physic  --> Simulink Output )/ s-ph (Simulink input --> Physic) Converter 
Coordinate Transform (Euler- Winkel): es gibt eine 4x4 Homogene Transformationsmatrix aus.
Signal Builder Block : erzeugt Bewegungssignale x,y,z  und theta ( Rotation des End Effektors).
Inverse Kinematics : es berechnet de Koordinaten der 5 Gelenke mit Gewichten (weights) 111100 (für das x,y,z, Roll, Pitch, Yaw) und InitialGuess 00000)
Forward Kinematics : liest die aktuelle Pose des Roboterarms aus
<img width="1261" height="491" alt="robotModel" src="https://github.com/user-attachments/assets/fe462154-e274-42e6-a952-606271042a47" />
<img width="1329" height="500" alt="simulink" src="https://github.com/user-attachments/assets/e0f07331-a2b6-4835-84cd-97d5acfde0f3" />

die Entfernungen des Gelenks des Roboterarms sind :

<img width="793" height="446" alt="fdgdfg" src="https://github.com/user-attachments/assets/6c10986d-e399-4a5c-ae83-686b24835877" />


# Homogene Tranformationsmatrix (4x4)

Translayionsvektor : (x,y,z)
Rotationsmatrix (3x3) Drehung um Roll,Pitch,Yaw : X,Y,Z axes
[0 0 0 1] Zeile zur Vereifachung der Berechnungen

T =[          x
        R     y
              z
      0  0  0 1 ]

# Bewegung und Regelung

Drehmoment (Torque) : automatisch Berechnet
Bewegung (Motion) : über Eigangssignale vorgegeben

PID Regelung :
P (Proportional) : Korrektur des Richtungsfehlers ( schrittweise Erhöhung)
I (Integral) : Ausgleich des kumulativen Fehlers über die Zeit
D (Derive) : Redezierung von Schwingungen ( Oscillations)

Negative Feedback Loops für jedes Gelenk zur Stabilisierung der Bewegung


# Ablauf des Endeffektors

Bewegt sich zu 4 Schraublöchern
Dreht sich um die Schrauber zu fixieren
Sieht sich nach der Aufgabe Zurück
<img width="963" height="483" alt="adazd" src="https://github.com/user-attachments/assets/d4249aa9-4a75-4bde-b811-2073014d665e" />


#Codegenerierung 

ROS Codegenierung  oder Hardware Toolbox für Implementierung in C /C++
Direkter Builde fur HardwareKomponenten möglich Ctrl+B

# Hinweise

In der Simulation konnen sCHWingungen auftreten, die durch der PID Controller Parameters oder Automatisch mit Tuning minimiert werden.
<img width="853" height="653" alt="output xy" src="https://github.com/user-attachments/assets/4903ea19-0c07-480d-802b-383f623b7e98" />



