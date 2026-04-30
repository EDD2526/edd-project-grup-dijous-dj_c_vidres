View this project on [CADLAB.io](https://cadlab.io/project/30197).

# Projecte DJ_C_Vidres (Portes)

> **Autors: Gurpinder Singh Kaur, Adria Pelegri Sabate**  
> **Versió: 4**

---

## Objectiu

PCB per al control d’un sistema de porta i alçavidres d’un vehicle. La placa permet controlar el moviment del vidre i l’actuació de la porta mitjançant botons, gestionar motors amb drivers pont H, detectar finals de carrera i situacions de sobrecorrent, i comunicar-se amb altres sistemes del vehicle mitjançant CAN. També inclou mecanismes de protecció, regulació d’alimentació, programació/debug mitjançant ICSP i test points per facilitar la depuració.

---

## Diagrama de blocs

> **Nota:** substituir el nom del fitxer si la imatge té un altre nom o ruta dins del repositori.

![Diagrama de blocs](docs/Diagrama_blocs_v4.png)

---

## Descripció funcional dels blocs

### Alimentació

La placa s’alimenta a partir d’una entrada de 12 V del vehicle. Aquesta entrada està protegida mitjançant fusible, díode de protecció i TVS. A partir d’aquesta tensió es genera una línia de 5 V mitjançant un convertidor DC-DC LM2596S-5.0. Posteriorment, es genera una línia de 3.3 V mitjançant un regulador LM1117-3.3 per alimentar la lògica digital, el microcontrolador, el transceptor CAN i els perifèrics de baixa tensió.

### Microcontrolador

El sistema està controlat per un microcontrolador **PIC24HJ128GP504-I/PT** alimentat a 3.3 V. Aquest dispositiu gestiona les entrades de botons i sensors, genera les ordres de control dels drivers de motor, llegeix el senyal analògic de corrent, comunica amb el lector RFID i permet la comunicació amb altres sistemes mitjançant CAN.

La placa inclou connector de programació/debug ICSP amb les línies `MCLR`, `PGEC` i `PGED`.

### Drivers de motor

S’utilitzen dos drivers **VNH5019A-E** en configuració de pont H:

- un driver per al motor  de l’alçavidres;
- un driver per al motor actuador de la porta.

Cada driver permet controlar el motor en ambdós sentits mitjançant senyals digitals `INA`, `INB` i `PWM`. També proporciona senyals de diagnòstic que permeten detectar possibles errors de funcionament.

### Mesura de corrent i antiatrapament

La mesura de corrent es realitza mitjançant la sortida de current sense del driver VNH5019A-E. Aquest senyal s’envia a una entrada ADC del microcontrolador per detectar situacions de sobrecorrent. Aquesta informació permet implementar una funció de seguretat tipus antiatrapament en el motor de l’alçavidres.

### Inputs d’usuari i sensors

La placa incorpora entrades per a:

- botons de pujada i baixada de l’alçavidres;
- control de bloqueig/desbloqueig de porta;
- sensor de final de carrera;
- reset manual del sistema;

Les entrades digitals es connecten al microcontrolador mitjançant resistències de pull-up/pull-down segons la funcionalitat requerida.

### RFID

El sistema inclou connexió per a un lector RFID RC522. Aquest mòdul permet identificar l’usuari o autoritzar accions del sistema. La comunicació amb el microcontrolador es realitza mitjançant SPI.

### Comunicació CAN

La comunicació amb altres sistemes del vehicle es realitza mitjançant un transceptor **SN65HVD230**. El bus CAN disposa de les línies `CANH` i `CANL`, amb resistència de terminació de 120 Ω. També s’han afegit punts de test per facilitar la verificació del bus.

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
  - Control bidireccional mitjançant pont H
  - Control PWM

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

| Descripció | Referència / Model | Package | Datasheet | Proveïdor | Preu aprox. | Unitats |
| --- | --- | --- | --- | --- | --- | --- |
| Microcontrolador | PIC24HJ128GP504-I/PT | TQFP-44 | [Datasheet](https://ww1.microchip.com/downloads/en/DeviceDoc/70293G.pdf) | Microchip | 4,00 € aprox. | 1 |
| Regulador lineal 3.3 V | LM1117DT-3.3 | SMD | [Datasheet](https://www.ti.com/lit/ds/symlink/lm1117.pdf) | Mouser | 1,47 € | 1 |
| Convertidor DC-DC 5 V | LM2596S-5.0 | SMD | [Datasheet](https://www.ti.com/lit/ds/symlink/lm2596.pdf) | Mouser | 5,99 € | 1 |
| Driver pont H | VNH5019A-E | MultiPowerSO-30 | [Datasheet](https://www.st.com/resource/en/datasheet/vnh5019a-e.pdf) | Mouser | 7,93 € | 2 |
| Lector RFID | RC522 | Mòdul extern / connector | Datasheet online | ElectroComponents | 2,20 € | 1 |
| Transceptor CAN | SN65HVD230 | SMD | [Datasheet](https://www.ti.com/lit/ds/symlink/sn65hvd230.pdf) | Mouser | 1,87 € | 1 |
| Sensor final de carrera | SS-5GLD | Connector / sensor extern | Datasheet Omron | Mouser | 2,15 € | 1 |
| Cristall | 8 MHz | SMD / THT segons footprint | Datasheet fabricant | — | — | 1 |
| Fusible | Fusible entrada 12 V | SMD / THT segons footprint | Datasheet fabricant | — | — | 1 |
| Díode TVS | Protecció entrada | SMD | Datasheet fabricant | — | — | 1 |

---

## Disseny PCB

La PCB s’ha dissenyat a **dues capes**. S’ha intentat separar funcionalment la zona de potència i la zona lògica per reduir interferències i facilitar el routing.

### Criteris principals de disseny

- Zona de potència situada principalment a l’esquerra de la PCB.
- Microcontrolador situat a la zona central.
- Comunicacions CAN i connectors principals situats a la dreta.
- Inputs i botons situats a la zona inferior/superior.
- Pla de `VBAT_PROT` per alimentar els drivers de motor.
- Pla de `+3.3V` per alimentar la part digital.
- Separació entre `GND` i `GNDPWR`, unides en un punt controlat.
- Pistes de potència més amples que les pistes de senyal.
- Ús de vies de major diàmetre o múltiples vies en zones de retorn de potència quan l’espai ho permet.
- Test points accessibles per a alimentació, debug, CAN, PWM, diagnòstic i corrent.

### Zona del cristall

La zona del cristall s’ha dissenyat seguint les recomanacions del fabricant del microcontrolador:

- cristall situat a prop dels pins `OSC1` i `OSC2`;
- pistes `OSC+` i `OSC-` curtes;
- condensadors de càrrega pròxims al cristall;
- zona de GND al voltant del circuit oscil·lador;
- absència de pistes de senyal o potència dins la zona protegida del cristall.

### Bus CAN

El transceptor CAN s’ha col·locat pròxim al connector corresponent. Les línies `CANH` i `CANL` s’han mantingut curtes i amb una disposició simètrica. També s’ha incorporat una resistència de terminació de 120 Ω i punts de test per facilitar la verificació del bus.

---

## Test points

S’han afegit test points per facilitar la posada en marxa i la depuració de la placa. Els punts principals són:

- `TP_VBAT`: alimentació protegida de 12 V
- `TP_5V`: sortida del convertidor DC-DC
- `TP_3V3`: alimentació lògica
- `TP_GND`: massa lògica
- `TP_GNDPWR`: massa de potència
- `TP_MCLR`: reset/programació
- `TP_PGEC`: línia de clock ICSP
- `TP_PGED`: línia de dades ICSP
- `TP_CANH`: línia CANH
- `TP_CANL`: línia CANL
- `TP_CURRENT`: lectura de corrent
- `TP_PWM`: control PWM
- `TP_WDIAG`: diagnòstic del driver de finestra
- `TP_DDIAG`: diagnòstic del driver de porta

Aquests punts permeten verificar alimentació, comunicació, programació, control dels motors i diagnòstic sense modificar la placa.

---

## Software

### Eines utilitzades

- KiCad 9.0 o superior
- LTspice per a simulacions
- MPLAB X IDE per al desenvolupament del firmware

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
- Control de sentit mitjançant `INA` i `INB`

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
- Punts de test per a mesures elèctriques
- Verificació de senyals crítiques

---

## Verificació

Abans de la fabricació/entrega s’han revisat els punts següents:

- ERC del circuit esquemàtic:
  - 0 errors
  - 6 avisos revisats
- DRC de la PCB:
  - 0 errors
  - 0 avisos
- Connexió correcta dels plans `GND`, `GNDPWR`, `VBAT_PROT` i `+3.3V`.
- Connexió dels pins d’alimentació del microcontrolador.
- Desacoblament dels pins `VDD`, `AVDD` i `VCAP`.
- Separació entre zona de potència i zona lògica.
- Rutes de potència curtes i amples per als motors.
- Zona del cristall segons recomanacions del fabricant.
- Bus CAN curt i simètric.
- Serigrafia completa i llegible.
- Punts de test accessibles.

---
