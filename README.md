View this project on [CADLAB.io](https://cadlab.io/project/30197).

# Projecte DJ_C_Vidres (Portes)

> **Autors: Gurpinder Singh Kaur, Adria Pelegri Sabate**  
> **Versió: 5**

---

## Objectiu

PCB per al control d’un sistema de porta i alçavidres d’un vehicle. La placa permet controlar el moviment del vidre i l’actuació de la porta mitjançant botons, gestionar motors amb drivers pont H, detectar finals de carrera i situacions de sobrecorrent, i comunicar-se amb altres sistemes del vehicle mitjançant CAN. També inclou mecanismes de protecció, regulació d’alimentació, programació/debug mitjançant ICSP i test points per facilitar la depuració.

---

## Diagrama de blocs



![Diagrama de blocs](docs/Diagrama_blocs_versio_final.jpg)

---

## Descripció funcional dels blocs

### Alimentació

La placa s’alimenta a partir d’una entrada de 12 V del vehicle. Aquesta entrada està protegida mitjançant fusible, díode de protecció i TVS. A partir d’aquesta tensió es genera una línia de 5 V mitjançant un convertidor DC-DC LM2596S-5.0. Posteriorment, es genera una línia de 3.3 V mitjançant un regulador LM1117-3.3 per alimentar la lògica digital, el microcontrolador, el transceptor CAN i els perifèrics de baixa tensió.

### Microcontrolador

El sistema està controlat per un microcontrolador **PIC24HJ128GP504-I/PT** alimentat a 3.3 V. Aquest dispositiu gestiona les entrades de botons i sensors, genera les ordres de control dels drivers de motor, llegeix el senyal analògic de corrent, comunica amb el lector RFID i permet la comunicació amb altres sistemes mitjançant CAN.

La placa inclou connector de programació/debug ICSP amb les línies MCLR, PGEC i PGED.

### Drivers de motor

S’utilitzen dos drivers **VNH5019A-E** en configuració de pont H:

- Un driver per al motor  de l’alçavidres;
- Un driver per al motor actuador de la porta.

Cada driver permet controlar el motor en ambdós sentits mitjançant senyals digitals INA, INB i PWM.

### Mesura de corrent i antiatrapament

La mesura de corrent es realitza mitjançant la sortida de current sense del driver VNH5019A-E. Aquest senyal s’envia a una entrada ADC del microcontrolador per detectar situacions de sobrecorrent. Aquesta informació permet implementar una funció  tipus antiatrapament en el motor de l’alçavidres.

### Inputs d’usuari i sensors

La placa incorpora entrades per a:

- Botons de pujada i baixada de l’alçavidres
- Control de bloqueig/desbloqueig de porta
- Sensor de final de carrera


Les entrades digitals es connecten al microcontrolador mitjançant resistències de pull-up/pull-down segons la funcionalitat requerida.

### RFID

El sistema inclou connexió per a un lector RFID RC522. Aquest mòdul permet identificar l’usuari o autoritzar accions del sistema. La comunicació amb el microcontrolador es realitza mitjançant SPI.

### Comunicació CAN

La comunicació amb altres sistemes del vehicle es realitza mitjançant un transceptor **SN65HVD230**. El bus CAN disposa de les línies CANH i CANL.

---

## Requisits / Especificacions

### Alimentació

- Entrada principal: 12 V
- Sortida intermèdia: 5 V
- Alimentació lògica: 3.3 V
- Protecció d’entrada mitjançant fusible, díode i TVS

### Microcontrolador

- Model: PIC24HJ128GP504-I/PT
- Encapsulat: TQFP-44
- Alimentació: 3.3 V
- Programació/debug: ICSP
- Perifèrics utilitzats:
  - PWM per al control dels motors
  - ADC per a la lectura de corrent
  - SPI per al lector RFID
  - CAN per a la comunicació amb el vehicle
  - GPIO per a botons, sensors i diagnòstic

### Motors

- Motor alçavidres:
  - Alimentació: 12 V
  - Corrent màxim estimat: fins a 3 A

- Motor actuador de porta:
  - Alimentació: 12 V
  - Control bidireccional mitjançant pont H
  - Control PWM

### Funcionalitats principals

- Control bidireccional dels motors
- Control de velocitat mitjançant PWM
- Lectura de botons d’usuari
- Lectura de final de carrera
- Detecció de sobrecorrent
- Diagnòstic dels drivers de motor
- Comunicació CAN
- Connexió RFID
- Programació i debug mitjançant ICSP
- Test point per depuració

---

## Components principals

| # | Component | Valor | Quantitat | Footprint | Preu x1 (€) |
|---|---|---|---|---|---|
| 1 | Capacitor | 100nF | 12 | Capacitor_SMD:C_0805_2012Metric | 0,09 |
| 2 | Capacitor | 10uF | 6 | Capacitor_SMD:C_0805_2012Metric | 0,79 |
| 3 | Capacitor | 220uF | 1 | Capacitor_SMD:CP_Elec_8x10 | 0,46 |
| 4 | Capacitor | 22pF | 2 | Capacitor_SMD:C_0805_2012Metric | 0,67 |
| 5 | Capacitor | 100uF | 1 | Capacitor_SMD:CP_Elec_8x10 | 0,69 |
| 6 | Diode Schottky | - | 2 | Diode_SMD:D_SMB_Modified | 0,22 |
| 7 | Diode TVS | - | 1 | Diode_SMD:D_SMB_Modified | 0,66 |
| 8 | Fuse | - | 1 | Fuse:Fuse_1812_4532Metric | 0,45 |
| 9 | Connector | - | 2 | Connector_Dsub:DSUB-9_Pins_Horizontal_P2.77x2.84mm_EdgePinOffset4.9 | 3,89 |
| 10 | Connector | - | 1 | Connector_PinSocket_1.00mm:PinSocket_1x08_P1.00mm_Vertical | 0,80 |
| 11 | Connector | - | 1 | Connector_PinHeader_2.54mm:PinHeader_1x05_P2.54mm_Vertical | 0,24 |
| 12 | Connector | - | 4 | TerminalBlock:TerminalBlock_MaiXu_MX126-5.0-02P_1x02_P5.00mm | 0,09 |
| 13 | Inductor | 33uH | 1 | Inductor_SMD:L_10.4x10.4_H4.8 | 1,38 |
| 14 | Resistor | 120Ω | 1 | Resistor_SMD:R_0805_2012Metric | 1,08 |
| 15 | Resistor | 10kΩ | 10 | Resistor_SMD:R_0805_2012Metric | 1,08 |
| 16 | Resistor | 1kΩ | 1 | Resistor_SMD:R_0805_2012Metric | 1,08 |
| 17 | Switch | - | 1 | Button_Switch_SMD:SW_DPDT_CK_JS202011JCQN | 0,86 |
| 18 | Switch | - | 1 | Button_Switch_THT:SW_CK_JS202011CQN_DPDT_Straight | 0,74 |
| 19 | Switch | - | 1 | Button_Switch_SMD:SW_SPST_TL3342 | 0,50 |
| 20 | Micro | - | 1 | PIC24HJ128GP504-I_PT:QFP80P1200X1200X120-44N | 7,23 |
| 21 | Transceiver | - | 1 | PACKAGE_SO:SOIC-8_3.9x4.9mm_P1.27mm | 1,87 |
| 22 | Motor Drivers | - | 2 | Package_SO:ST_MultiPowerSO-30 | 7,93 |
| 23 | DC-DC | - | 1 | Package_TO_SOT_SMD:TO-263-5_TabPin3 | 5,99 |
| 24 | DC-DC | - | 1 | Package_TO_SOT_SMD:TO-252-3_TabPin2 | 1,12 |
| 25 | Crystal | 8MHz | 1 | Crystal:Crystal_SMD_3225-4Pin_3.2x2.5mm | 0,53 |



## Disseny PCB

La PCB s’ha dissenyat a **dues capes**. S’ha intentat separar funcionalment la zona de potència i la zona lògica per reduir interferències i facilitar el routing.

### Criteris principals de disseny

- Zona de potència situada principalment a l’esquerra de la PCB.
- Microcontrolador situat a la zona central.
- Comunicacions CAN i connectors principals situats a la dreta.
- Inputs i botons situats a la zona inferior/superior.
- Pla de VBAT_PROT per alimentar els drivers de motor.
- Pla de +3.3V per alimentar la part digital.
- Separació entre GND i GNDPWR
- Pistes de potència més amples que les pistes de senyal.
- Test points  per a alimentació, debug, CAN, PWM, diagnòstic i corrent.


### Bus CAN

El transceptor CAN s’ha col·locat pròxim al connector corresponent. Les línies `CANH` i `CANL` s’han mantingut curtes i amb una disposició simètrica.

---

## Test points

S’han afegit test points per facilitar la posada en marxa i la depuració de la placa. Els punts principals són:

- TP_VBAT: alimentació protegida de 12 V
- TP_5V: sortida del convertidor DC-DC
- TP_3V3: alimentació lògica
- TP_GND: massa lògica
- TP_GNDPWR: massa de potència
- TP_MCLR: reset/programació
- TP_PGEC: línia de clock ICSP
- TP_PGED: línia de dades ICSP
- TP_CANH: línia CANH
- TP_CANL: línia CANL
- TP_CURRENT: lectura de corrent
- TP_PWM: control PWM
- TP_WDIAG: diagnòstic del driver de finestra
- TP_DDIAG: diagnòstic del driver de porta

Aquests punts permeten verificar alimentació, comunicació, programació, control dels motors i diagnòstic sense modificar la placa.

---

## Software

### Eines utilitzades

- KiCad 9.0
- LTspice per a simulacions

### Configuració prevista del microcontrolador

- PWM per al control dels drivers de motor
- ADC per a lectura del senyal de corrent
- SPI per al lector RFID
- CAN per a comunicació amb el vehicle
- GPIO per a botons, sensors, finals de carrera i diagnòstic
- ICSP per a programació i debug

### Funcionalitats previstes

#### Control de motors

- Control de pujada i baixada del vidre
- Control d’actuació de la porta
- Control de velocitat mitjançant PWM
- Control de sentit mitjançant INA i INB

#### Seguretat

- Detecció de sobrecorrent
- Funció antiatrapament
- Lectura de final de carrera
- Diagnòstic dels drivers de motor

#### Comunicació

- Comunicació CAN amb altres sistemes del vehicle
- Comunicació SPI amb el lector RFID

#### Debug

- Programació mitjançant ICSP
- Test points per a mesures elèctriques


---

## Verificació

Abans de la fabricació/entrega s’han revisat els punts següents:

- ERC del circuit esquemàtic:
  - 0 errors
  - 6 avisos 
- DRC de la PCB:
  - 0 errors
  - 0 avisos
- Separació entre zona de potència i zona lògica.
- Bus CAN curt i simètric.
- Serigrafia completa i llegible.
- Test points accessibles.

---
