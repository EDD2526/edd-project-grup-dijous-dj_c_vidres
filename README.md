View this project on [CADLAB.io](https://cadlab.io/project/30197). 

# Projecte DJ_C_Vidres (Portes)

>**Autors: Gurpinder Singh Kaur, Adria Pelegri Sabate**  
>**Versió: 4**

----------

## Objectiu

>PCB per al control del sistema d’alçavidres d’un vehicle. El sistema permet controlar el moviment del vidre mitjançant botons, detectar finals de carrera i situacions de sobrecorrent, i comunicar-se amb altres sistemes del vehicle mitjançant CAN. També inclou mecanismes de protecció i regulació d’alimentació.

---

## Diagrama de blocs
![Diagrama de blocs](C:\Users\adpes\Documents\Projecte_eines_disseny\edd-project-grup-dijous-dj_c_vidres\Diagrama_blocs_v.4.)

### Descripció/funcionalitat de cada bloc

* **Alimentació**
  - Entrada de 12V protegida amb fusible, díode i TVS.
  - Conversió a 5V amb convertidor DC-DC (LM2596).
  - Regulació a 3.3V amb LM1117 per alimentar la part digital.

* **Microcontrolador**
  - PIC24HJ128GP502.
  - Gestiona totes les entrades i sortides.
  - Controla el driver del motor mitjançant senyals PWM i digitals.
  - Llegeix sensors digitals i analògics.

* **Driver de motor**
  - VNH5019A-E (pont H).
  - Permet controlar el motor de l’alçavidres en ambdós sentits.
  - Control per senyals INA, INB i PWM.
  - Proporciona senyals de diagnòstic.

* **Sensor de corrent**
  - Mesura del corrent del motor mitjançant resistència shunt.
  - Permet implementar protecció antiatrapament.

* **Inputs (usuari i servei)**
  - Botons de pujada i baixada.
  - Sensor de final de carrera.
  - Reset manual.
  - Connector de programació ICSP.

* **RFID**
  - Lector RC522 per identificar usuari.

* **Comunicació CAN**
  - Transceptor SN65HVD230.
  - Permet integració amb el bus del vehicle.

---

## Requisits / Especificacions

* Alimentació:
  - Entrada: 12V
  - Sortides: 5V i 3.3V

* Microcontrolador:
  - PIC24HJ128GP502
  - Alimentació: 3.3V

* Motor alçavidres:
  - 12V @ fins a 3A

* Funcionalitats:
  - Control bidireccional del motor
  - Control PWM
  - Lectura de botons i sensors
  - Detecció de sobrecorrent
  - Comunicació CAN

---

## Components

| Descripci&#243; | Ref | Package |Datasheet | Prove&#239;dor | Preu | Unitats |
| --- | --- | --- | --- | ---| --- | --- |
| Microcontrolador | PIC24HJ128GP502 | SOIC-28 |[Datasheet](https://ww1.microchip.com/downloads/en/DeviceDoc/70292G.pdf) | [Microchip](https://www.microchip.com) | 4,00€ aprox | 1x |
| Regulador| LM1117 3.3V | SMD | [Datasheet](https://www.ti.com/lit/ds/symlink/lm1117.pdf) | Mouser | 1,47€ | 1x |
| DC - DC | LM2596S-5.0 | SMD | [Datasheet](https://www.ti.com/lit/ds/symlink/lm2596.pdf) | Mouser | 5,99€ | 1x |
| H-Bridge | VNH5019A-E |---| [Datasheet](https://www.st.com/resource/en/datasheet/vnh5019a-e.pdf)| Mouser | 7,93€| 1x |
| Lector RFID | RC522 |---| Datasheet online | ElectroComponents | 2,20€| 1x |
| Transceptor CAN | SN65HVD230 |---| Datasheet TI | Mouser | 1,87€| 1x |
| Sensor final de carrera | SS-5GLD |---| Datasheet Omron | Mouser | 2,15€| 1x |

---

## Software

### Eines:

* KiCad 9.0 o superior
* LTspice (simulacions)
* MPLAB X IDE

### Configuraci&#243; :

* Configuració del microcontrolador:
  - PWM per control del motor
  - ADC per lectura de corrent
  - SPI per RFID
  - CAN per comunicació
  - ICSP per programació

### Funcionalitats:

* Control del motor:
  - Pujada i baixada amb botons
  - Control de velocitat amb PWM

* Seguretat:
  - Detecció de sobrecorrent
  - Final de carrera

* Comunicació:
  - CAN bus

* Debug:
  - Programació ICSP