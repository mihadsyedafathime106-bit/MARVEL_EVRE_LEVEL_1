#EV-RE LEVEL 1 REPORT
## TASK 1:555 Timer Astable Multivibrator Simulation & PCB Design

---

## 1. Objective
* **LTspice:** Simulate a 555 astable multivibrator to observe oscillation frequency, pulse widths ($T_{\text{HIGH}}$, $T_{\text{LOW}}$), and duty cycle.
* **KiCad:** Design a schematic for an LED blinking circuit and layout a 2-layer PCB with routed traces and footprint assignments.

---

## 2. Working Steps

### Part A: LTspice Simulation
1. **Schematic Entry:** Place the `NE555` timer, resistors, capacitors, LED, and $9\text{V}$ DC supply. Wire Pin 7 between $R_1$/$R_2$, Pins 2 & 6 between $R_2$/$C_1$, and Pin 3 to $R_{\text{LED}}$ + LED.
2. **Transient Analysis Setup:** Add `.tran 0 1s 0 100us`.

![Capacitor Charging vs Output Waveform](images/task1b.png)

### Part B: KiCad PCB Design
* Define board boundary ($40\text{mm} \times 30\text{mm}$) on `Edge.Cuts`.
   * Place IC centrally; keep $R_1, R_2, C_1$ close to Pins 2, 6, and 7.
   * Route signal tracks ($0.3\text{mm}$) at $45^\circ$ angles and power tracks ($0.6\text{mm}$) on Top layer (`F.Cu`).
  
   ![Circuit Design: 555 Astable Multivibrator Schematic](images/task1a.png)
   ![Component Footprints](images/task1c.png)
   ![Final 3D PCB Prototype & Routing](images/task1d.png)
### 3. Learning Outcomes
1. **SPICE Simulation & EDA Workflows:** Gained a complete practical understanding of computer-based circuit modeling in LTspice and end-to-end electronic engineering workflows in KiCad.
2. Understood PCB layouting and routing

# Task 2 – Point Turn of a Vehicle with Ultrasonic Sensor

## Objective
To interface an **HC-SR04 ultrasonic sensor** with Arduino and demonstrate obstacle detection for an obstacle-avoiding vehicle.

## Components
- Arduino Uno
- HC-SR04 Ultrasonic Sensor
- SG90 Servo Motor
- Breadboard and jumper wires
- USB cable

## Connections

| Component | Arduino |
|---|---|
| HC-SR04 VCC | 5V |
| HC-SR04 GND | GND |
| Trig | Pin 9 |
| Echo | Pin 10 |
| Servo Signal | Pin 6 |
| Servo VCC/GND | 5V/GND |

## Working
The HC-SR04 sends ultrasonic waves and measures the returning echo to calculate the distance of an obstacle. The SG90 servo rotates the sensor to scan different directions. The detected distance can be used to determine a change in direction for an obstacle-avoiding vehicle.
distance=(time*speed)/2

## Outcome
Successfully demonstrated **obstacle detection and servo-based scanning**. The complete motorized vehicle and point-turn mechanism were not implemented.

## Performance Video
[SEE MY WORK HERE ](https://youtube.com/shorts/vrj4dnTEFtE?si=NLritdF1-pOrneIa)


# Task 3 – Temperature and Humidity Detection

## Objective
To measure temperature and humidity using **LM35 and DHT11 sensors**, and indicate high temperature using an **LED controlled by a BJT**.

## Components & Purpose

| Component | Purpose |
|---|---|
| **LM35** | Measures temperature as an analog voltage (10mV/c)|
| **DHT11** | Measures temperature and humidity digitally |
| **BJT (BC547/2N2222)** | Acts as an electronic switch to control the LED |
| **LED** | Indicates when the temperature crosses the set threshold |
| **Arduino Uno** | Processes sensor readings and controls the circuit |


## Connections

| Component | Arduino |
|---|---|
| LM35 VCC | 5V |
| LM35 Vout | A0 |
| LM35 GND | GND |
| DHT11 VCC | 5V |
| DHT11 DATA | D7 |
| DHT11 GND | GND |
| BJT Base | D8 through 1kΩ |
| LCD | Arduino digital pins |

## Working
The **LM35** detects temperature and provides an analog output to Arduino. The **DHT11** measures temperature and humidity and sends digital data to Arduino. When the LM35 temperature exceeds the set threshold, Arduino activates the **BJT**, which switches ON the LED. The temperature and humidity values are displayed on the **serial monitor**.

## Outcome
Successfully demonstrated **analog and digital sensor interfacing**, threshold-based switching using a BJT, and real-time temperature and humidity display.

## Performance Video
[YouTube Video](https://youtube.com/shorts/a7KXjhxDUIg?si=-qdTFoT_1tfb0kIH)


# Task 5 – Battery Capacity Measurement

## Objective
To monitor the voltage of a **18650 Li-ion battery** using Arduino and use a **MOSFET as a switch** to disconnect the load when the battery voltage falls below a safe threshold.

## Components & Purpose

| Component | Purpose |
|---|---|
| **Arduino Uno** | Monitors battery voltage and controls the MOSFET |
| **18650 Li-ion Cell** | Battery under test |
| **N-Channel MOSFET** | Acts as a switch to control the load |
| **10Ω, 5W Resistor** | Acts as the load during battery discharge |
| **220Ω Resistor** | Protects the Arduino output pin |
| **10kΩ Resistor** | Keeps the MOSFET OFF when Arduino resets |
| **Multimeter** | Used for voltage measurement and calibration |
| **Breadboard & Jumper Wires** | Circuit connections |

## Connections

| From | To |
|---|---|
| Battery (+) | Arduino A0 + 10Ω resistor |
| Other end of 10Ω resistor | MOSFET Drain |
| MOSFET Source | Arduino GND + Battery (−) |
| Arduino D2 | 220Ω → MOSFET Gate |
| MOSFET Gate | 10kΩ → GND |

## Working
Arduino continuously monitors the **battery voltage through analog input A0**. The MOSFET controls the discharge load connected to the battery. When the battery voltage falls below the defined safe threshold, Arduino switches OFF the MOSFET, disconnecting the load and preventing further discharge.

## Outcome
Successfully demonstrated **battery voltage monitoring and basic battery protection logic** using Arduino and a MOSFET.

![Battery Circuit Setup](images/task5c.jpeg)
Arduino output 
```text
Time(s), Voltage(V), Current(mA), Capacity(mAh)
1,       3.120,      312.0,       0.09
30,      3.090,      309.0,       2.59
60,      3.060,      306.0,       5.15
120,     3.030,      303.0,       10.23
180,     3.015,      301.5,       15.27
240,     3.002,      300.2,       20.28
295,     2.998,      299.8,       24.87
300,     2.995,      299.5,       25.29
--- CUTOFF: battery reached safe limit (3.00V threshold), load disconnected ---

```
# Task 6 – Battery Charging

## Objective
To charge a **Li-ion battery using a solar panel and a solar charging module**, demonstrating the practical use of solar energy for battery charging.

## Components & Purpose

| Component | Purpose |
|---|---|
| **Solar Panel** | Converts sunlight into electrical energy |
| **TP4056 Solar Charging Module** | Regulates the solar power and safely charges the Li-ion battery |
| **Li-ion Battery** | Stores the generated electrical energy |

## Working
The **solar panel** converts sunlight into electrical energy. This output is connected to the **solar charging module**, which regulates the charging process and supplies suitable power to the Li-ion battery.

## Outcome
Successfully demonstrated **solar-based Li-ion battery charging** and understood the practical implementation of a solar charging system.
![charging of battery under sunlight](images/task6.jpeg)
# Task 7 – Solar Tracker

## Objective
To build a simple **solar tracking system** using LDRs, Arduino, and a servo motor to orient a solar panel toward the strongest light source.

## Components & Purpose

| Component | Purpose |
|---|---|
| **Arduino Uno** | Processes LDR readings and controls the servo |
| **LDRs** | Detect and compare the intensity of light |
| **Servo Motor** | Rotates the solar panel toward stronger light |
| **Solar Panel** | Receives light for solar energy collection |
| **Resistors** | Form voltage-divider circuits with the LDRs |
| **Breadboard & Jumper Wires** | Circuit connections |

## Working
The two **LDRs** detect the intensity of light from different directions. Arduino compares their readings and controls the **servo motor** accordingly. The servo rotates the solar panel toward the LDR receiving stronger light, helping the panel remain aligned with the light source.
## Outcome
Successfully demonstrated **automatic light tracking using dual LDR comparison and servo control**, showing how solar tracking can improve the collection of available sunlight.
## Performance Video

[YouTube Video](https://youtube.com/shorts/QJGWhb2LBig?si=nJiAUpGKdG_2ZUgr)

# Task 8 – Simple Electric Circuits Simulation on MATLAB

## Objective
To learn the basics of **MATLAB Simulink** by designing and simulating simple electrical circuits and analyzing their voltage and current waveforms.

## Software Used
- MATLAB
- Simulink

## Working
The circuit models were created using **Simulink blocks** and simulated over time. Different input signals and circuit elements were used to observe their responses. The **Scope** blocks were used to visualize the resulting voltage and current waveforms.

## Output
The simulation successfully produced the expected **sinusoidal, switching, and current waveforms**. The Scope outputs were used to analyze how the circuit signals vary with time.

## Outcome
Successfully demonstrated **basic circuit modeling in MATLAB Simulink** and learned to observe and analyze electrical waveforms using simulation.

## Simulation Outputs

### Simulink Circuit Model
![Simulink Circuit Model](images/task8b.png)

### Voltage and Switching Waveforms
![Voltage and Switching Waveforms](images/task8c.png)

### Multiple Waveform Analysis
![Multiple Waveform Analysis](images/task8d.png)

### Signal Analysis
![Signal Analysis](images/task8e.png)

# Task 10 – Auto Night Lamp Using LED for Electric Vehicles

## Objective
To design an automatic light-sensitive LED circuit using an **LDR and BJT transistor**, simulating an automatic headlamp system for electric vehicles.

## Components & Purpose

| Component | Purpose |
|---|---|
| **LDR** | Detects the surrounding light intensity |
| **BJT Transistor** | Acts as a switch to control the LED |
| **LED** | Acts as the automatic headlamp |
| **Resistors(10kohm and 220ohm)** | Control current and set the switching threshold |
| **Breadboard & Jumper Wires** | Circuit connections |

## Working
The **LDR** senses the surrounding light level. When sufficient light is present, the LED remains OFF. When the light level decreases, the BJT switches ON and the **LED lights up automatically**. A mobile flashlight was used to simulate changing light conditions.

## Outcome
Successfully demonstrated an **automatic night lamp system** that responds to changes in light intensity, simulating an EV automatic headlamp.

## Circuit Setup

![Auto Night Lamp Circuit](images/task10.jpeg)


## Performance Video
[YouTube Video](https://youtube.com/shorts/UPNs90nFizU?si=LjqsDYSlyMt0oDU0)
# Task 11 – Buck Converter on LTspice

## Objective
To design and simulate a **DC-DC buck converter** in LTspice and observe the conversion of a higher DC voltage into a lower DC output voltage.

## Components/Blocks Used
- DC Voltage Source
- MOSFET/Switch
- Diode
- Inductor
- Capacitor
- Load Resistor
- Voltage and Current Probes
- LTspice Simulation Environment

## Working Steps
1. A DC input voltage is applied to the buck converter circuit.
2. The switching device rapidly turns ON and OFF to control the energy delivered to the circuit.
3. The inductor stores energy during the ON state and releases it during the OFF state.
4. The diode provides a current path when the switch is OFF.
5. The capacitor smooths the output voltage.
6. LTspice is used to observe the input voltage, output voltage, and inductor current waveforms.

## Learning Outcomes
- Understood the basic working of a **buck converter**.
- Observed step-down DC voltage conversion through simulation.
- Learned to analyze **output voltage and inductor current waveforms** using LTspice.
- Gained basic understanding of switching operation in power converters.

## Simulation Outputs

![Buck Converter Simulation](images/task11b.png)

![Voltage and Current Waveforms](images/task11a.png)
# Task 12 – Wireless Charger Simulation on Tinkercad

## Objective
To simulate the basic principle of **wireless power transfer** using transmitter and receiver coils in Tinkercad.

## Components/Blocks Used
- Transmitter Coil
- Receiver Coil
- AC/Power Source
- LED
- Resistors
- Tinkercad Simulation Environment

## Working Steps
1. A changing electrical signal is applied to the transmitter coil.
2. The changing current produces a changing magnetic field.
3. The magnetic field induces voltage in the nearby receiver coil.
4. The induced electrical energy is used to power the LED.
5. The LED provides a visual indication of wireless power transfer.

## Learning Outcomes
- Understood the basic principle of **electromagnetic induction**.
- Learned how electrical energy can be transferred without a direct wired connection.
- Gained basic knowledge of the working principle of **wireless charging systems**.

## Simulation Output

![Wireless Charger Simulation](images/task12.png)
# Task 13 – Transistors as Switches and Voltage Regulators

## Objective
To understand the use of a **transistor as an electronic switch** and observe the voltage drop introduced by a transistor in a simple circuit.

## Components/Blocks Used
- Arduino
- NPN Transistor
- LED
- Resistors
- DC Supply
- Tinkercad Simulation

## Working Steps
1. Arduino sends a digital HIGH or LOW signal to the transistor base.
2. When the base signal is HIGH, the transistor switches ON and allows current to flow through the LED.
3. When the signal is LOW, the transistor switches OFF and the LED turns OFF.
4. A second circuit is simulated to observe the voltage across the LED with the transistor included.
5. The measured voltage is compared to understand the voltage drop across the transistor.

## Learning Outcomes
- Understood how a **transistor works as an electronic switch**.
- Learned how a digital signal can control a higher-current load.
- Observed voltage drop in a transistor-based circuit.
- Gained basic knowledge relevant to transistor-based power control and regulation.

## Simulation Outputs

### Transistor as a Switch
The first simulation demonstrates the transistor switching the LED circuit, with a measured voltage of approximately **1.95 V**.

![Transistor as a Switch](images/task13a.png)

### Voltage Drop Using Transistor
The second simulation demonstrates the voltage reduction across the LED circuit after introducing the transistor, with a measured voltage of approximately **1.75 V**.

![Transistor Voltage Drop](images/task13b.png)

## Performance Video

[YouTube Video](https://youtu.be/lowGF4Ue7jY?si=v4rK2mrr6qyVFhfD)
# Task 14 – LED Brightness Control Using PWM and MOSFET

## Objective
To control LED brightness using **Arduino PWM and an N-channel MOSFET**, demonstrating efficient electronic switching and power control.

## Components Used
- Arduino Uno
- N-Channel MOSFET
- LED
- Resistor
- Jumper Wires
- Breadboard

## Working Steps
1. Arduino generates a PWM signal from a digital PWM pin.
2. The PWM signal is applied to the MOSFET gate.
3. The MOSFET switches the LED current ON and OFF rapidly.
4. The PWM duty cycle determines the average power delivered to the LED.
5. Increasing the duty cycle increases LED brightness, while decreasing it makes the LED dimmer.

## Learning Outcomes
- Understood **PWM-based brightness control**.
- Learned how an N-channel MOSFET operates as an electronic switch.
- Understood the relationship between **PWM duty cycle and power delivery**.
- Gained practical knowledge of MOSFET switching used in power-electronic applications.

## Performance Video

[YouTube Video](https://youtube.com/shorts/ha99GT3NzEo?si=7Q8ndRpahtwOng-K)

# Task 15 – AC to DC Conversion and Observing Direct DC vs. Rectified DC

## Objective
To simulate AC-to-DC conversion principles by applying a pulsating high-frequency square wave (Arduino PWM) through a rectifier diode and smoothing capacitor to compare raw vs. filtered DC output

## Components Used
- Arduino Uno
- Diode
- Capacitor
- Green LED
- Resistor
- Jumper wires
- Breadboard

## Working
The Arduino generates a high-frequency pulsating DC signal via PWM ($0-5\text{ V}$). Although PWM is unidirectional, it models the single-polarity pulses of a half-wave rectified AC signal.Diode Behavior: The single diode introduces a standard forward voltage drop ($V_D \approx 0.7\text{ V}$) and prevents reverse current flow.Capacitor Filtering: A parallel smoothing capacitor stores energy during the PWM pulse HIGH phase and discharges into the load during the LOW phase, converting high-frequency pulses into a steady average DC voltage with minimal ripple ($V_{ripple} \approx \frac{I_{load}}{f \cdot C}$)

## Tests

### Test 1 – Direct DC Power
Arduino 5V is connected directly to the input node. The LED glows with **maximum and steady brightness**.

![Direct DC Output](images/TASK15.jpeg)

### Test 2 – Unfiltered Rectified DC
The diode is connected between the Arduino PWM output and input node, with the capacitor removed. The LED appears **dimmer and may flicker** due to the pulsating output and diode voltage drop.


### Test 3 – Filtered Rectified DC
The capacitor is connected across the input node and GND. The LED becomes **brighter and steadier** than Test 2 as the capacitor reduces voltage fluctuations.

[YouTube Video – Unfilteered vs Filtered Rectified DC](https://youtube.com/shorts/-65GE5MlFZA?si=0HR0lpqnP8nsLrED)

## Learning Outcomes
- Understood the basic principle of **AC to DC conversion**.
- Learned how a diode performs **half-wave rectification**.
- Understood the role of a capacitor in **filtering and smoothing DC**.
- Compared the output of direct DC, unfiltered rectified DC, and filtered rectified DC.
- Observed the effect of diode voltage drop and ripple on LED brightness.