# 555 Timer Monostable Multivibrator
### 1. AIM
Generate a waveform with pulse width of 0.5 ms under different trigger conditions using 555 timer IC 

### 2. THEORY
The NE555 timer is a versatile IC used in a variety of timing applications. It can be operate in three primary modes:       
- **Astable Mode**: No stable state; the timer continuously switches between HIGH and LOW, producing a square wave.
- **Monostable Mode**: One stable state (LOW); the timer produces a single output pulse in response to an external trigger.
- **Bistable Mode**: Two stable states, toggled by external signals.
In the monostable mode, when a **falling edge** is applied to the **Trig** pin, the output goes HIGH for a period defined by external resistor (R) and capacitor (C), then automatically returns to LOW.<br>
In monostable mode, the 555 timer has one stable state (output LOW) and one quasi-stable state (output HIGH). The circuit remains in its stable state until an external trigger is applied. When triggered, the timer output goes HIGH for a predetermined duration and then automatically returns to LOW.<br>
### Pulse Duration<br>
The duration (T) of the output HIGH pulse is determined by an external resistor (R) and capacitor (C):<br>
t=
1.1
×
𝑅
×
𝐶
 (in seconds)
Where:

𝑅
R is in ohms (Ω)

𝐶
C is in farads (F)
### circuit diagram<br>
![image](https://github.com/user-attachments/assets/06633681-e358-45ec-a27c-b9b5a456154f)<br>
### Features of 555 Monostable Mode<br>
Easy to implement<br>

Accurate timing control (depending on R and C)<br>

Output automatically resets after the time delay<br>
#### Target pulse width:

*T = 0.5 ms*

Using the monostable formula:

*T = 1.1 x R x C*

Assuming:
- C = 1 µF

Then:

*R = T/1.1 x C = 454.54 Ω

Can be retriggered if necessary (with added circuitry)<br>
Selected values:
- R = 454.54 Ω
- C = 1 µF

These values yield a pulse duration of approximately 0.5 ms.<br>
### 4. SIMULATION ANALYSIS
#### diagram<br>
![image](https://github.com/user-attachments/assets/053e9390-ceba-4e3c-b5a6-9bfb1ee1f6ba)<br>
### <ins>Transient Analysis
Used to verify timing behaviour of the output signal in response to various trigger signals

### <ins>Procedure 
1. Open LTspice and create a new schematic.Set up the circuit as per the circuit diagram.
2. Select the Resistor (R) and Capacitor(C) as per the given specifcation.
3. Simulation Command
   - Go to **Simulate** -> *Edit Simulation Cmd*
   - Choose **Transient**, and set thime as needed per case.
   - ### <ins>Case 1: Properly Spaced Triggers
- Trigger Pulse Source:
  VTrig PULSE(5 0 0.05m 0 0 0.01m 2m)
  - This generates a falling edge every 2 ms (well spaced).

- Run the simulation for 10 ms.
- ![image](https://github.com/user-attachments/assets/8a213978-23d0-46eb-82ad-00fcad7c3c40)
- **Expected Output**:
  - Each falling edge triggers the 555.
  - Output (VOUT) goes HIGH for approx. 0.5 ms on each trigger.
  - Multiple output pulses will be seen.
    ### <ins>Case 2: Rapid Repeated Triggers
- Trigger Pulse Source:
  VTrig PULSE(5 0 0.05m 0 0 0.01m 0.2m)
  - This generates a falling edge every 0.2 ms (faster than output duration).

- Run the simulation for 2 ms.
- ![image](https://github.com/user-attachments/assets/4f736798-ac6e-41fc-819e-158a00794079)
- **Expected Output**:
  - First falling edge triggers the 555.
  - Output (VOUT) goes HIGH for 0.5 ms.
  - All triggers during this HIGH time are ignored.
    ### inference
    The experiment confirms that the 555 timer IC, when configured in monostable mode, reliably produces a single output pulse of approximately 0.5 ms duration upon receiving a valid 
    negative-going trigger pulse.<br>
    The timer exhibits non-retriggerable behavior, meaning it does not respond to additional trigger inputs while the output pulse is still HIGH. This ensures that the output pulse 
    duration remains fixed and is not extended or interrupted by any subsequent triggers during the active period. This behavior is critical for applications requiring precise timing 
    and pulse shaping.<br>
    Triggering the timer using a mechanical push-button can introduce issues such as contact bounce, potentially leading to multiple unintended triggers. To mitigate this, a debouncing 
    mechanism or edge-filtering logic (e.g., using an RC filter or Schmitt trigger) is recommended for clean and accurate triggering.<br>
    For continuous triggering applications, such as periodic pulse generation or automation testing, feeding the monostable circuit with an astable multivibrator output (e.g., from 
    another 555 timer or a microcontroller) ensures consistent operation. Incorporating logic gates or edge-detection circuits further enhances trigger reliability and prevents overlap 
    or invalid re-triggering.<br>
    Overall, the results validate that the 555 timer in monostable mode is well-suited for timing, pulse generation, and event-response applications, where a precise and non- 
    retriggerable pulse is required after each valid input trigger.<br>
    
### conclusion
   
During testing and analysis, the timer exhibited non-retriggerable behavior, meaning it ignores any subsequent trigger pulses while the output is HIGH. This ensures stable and 
    predictable timing, making the 555 timer highly suitable for digital timing, delay, and pulse-generation applications.<br>
    The circuit's response was further evaluated under different trigger scenarios:
    Clean, single triggers reliably initiated the timing pulse.<br>
    Rapid or noisy inputs, such as mechanical switch bounce, revealed the importance of input signal conditioning, such as debouncing or edge-filtering circuits.<br>
    Automated triggering was effectively demonstrated using an astable signal source, where external logic (like Schmitt triggers or gating circuits) can enhance performance and prevent 
    false or overlapping triggers.<br>
    Overall, the monostable 555 timer circuit proves to be a versatile and robust solution for a wide range of timing applications. Its behavior is well-understood, easy to simulate, 
    and predictable in both hardware and software environments. With proper design considerations, it can be extended for use in sequential logic systems, time-delay circuits, pulse- 
    width modulation (PWM), and event-driven automation.<br>
    # Astable Multivibrator And Monostable Multivibrator Using 555 Timer ICs
### 1. AIM
Generate a waveform with pulse width of 0.5 ms under different trigger conditions using 555 timer IC.

### 2. THEORY
An Astable Multivibrator is a circuit that coontinuously switches between two unstable states without requiring any external triggering. It operates as a self-oscillating square wave output, which is ideal for applications like clocks, pulse generation, and frequency synthesis.

In most implementations, the 555 timer IC is often used to create an astable multivibrator. In this mode, the 555 timer works by charging and discharging a capacitor through resistors, which results in the generation of a periodic square wave.

### <ins>Logic Structure Used
To ensure proper, clean triggering of the monostable 555 timer, the following logic sequence is used:
- **Astable Multivibrator (Trigger Source)**: Produces regular square wave pulses.
- **Differentiator Circuit**: Converts edges of the sqaure wave into narrow spikes.
- **Clipper Circuit**: Allows only negative spikes to pass, rejecting positive ones.
- **Monostable Multivibrator (Main 555 Timer)**: Generates a fixed-output pulse (0.5 ms) on each valid trigger.
   
### 3. WORKING PRINCIPLE OF THE ASTABLE MULTIVIBRATOR
### 1. Charging Phase:
- The capacitor charges through R1 and R2.
- When the capacitor voltage reaches 2/3 of Vcc, the internal comparator resets the flip-flop.
- The output goes LOW.

### 2. Discharging Phase:
- The capacitor discharges through R2 only (through pin 7).
- When the voltage drops to 1/3 of Vcc, the comparator sets the flip-flop.
- The output goes HIGH, and the cycle repeats.

This cycle of charging and discharging creates a continuous square wave.

### Output Characteristics:
- The frequency of the oscillation depends on R1, R2 and C:

  *Frequency = 1.44/(R1 + 2 x R2) X C*

  *Duty Cycle = R1 + R2/R1 + 2 X R2*

### Key Features
| Feature                            | Description                                                           |
| ---------------------------------- | --------------------------------------------------------------------- |
| **Free-Running Operation**      | Continuously generates square waves without external triggering.      |
| **Adjustable Frequency**        | Frequency and duty cycle can be set by choosing R1, R2, and C values. |
| **Square Wave Output**          | Suitable for use as a clock pulse, blinking LED, or timing trigger.   |
| **No Stable State**             | Keeps switching between HIGH and LOW—never settles.                   |
| **Used in Timing Applications** | Often used in timers, oscillators, LED blinkers, and digital clocks.  |
| **Simple Circuit**              | Can be built using a 555 timer, 2 resistors, and 1 capacitor.         |
| **Reliable and Cost-Effective** | Easy to implement with stable operation over a wide voltage range.    |

### 4. CIRCUIT DESIGN AND CALCULATION
### <ins> Calculations
### Astable Multivibrator
*ton = 0.69 (R1 + R2)C2*,   *toff = 0.69 x R1 x C2*

#### <ins>Case 1:
Consider ton = 0.3 ms, toff = 0.2 ms and C2 = 0.01 µF

*R2 = 0.2 x 10^-3/0.69 x 0.01µ = 28.985k Ω*

*R1 = (0.3 x 10^-3/0.69 x 0.01µ) - 28.985k = 14.493k Ω*

#### <ins>Case 2:
Consider ton = 0.7 ms, toff = 0.3 ms and C2 = 0.01 µF

*R2 = 0.3 x 10^-3/0.69 x 0.01µ = 43.478k Ω*

*R1 = (0.7 x 10^-3/0.69 x 0.01µ) - 43.478k = 57.971k Ω*

#### <ins>Case 3:
Consider ton = 0.1 ms, toff = 0.4 ms and C2 = 0.01 µF
This is not possible as ton must be greater than toff in astable multivibrator. Thus consider ton = 0.4 ms and toff = 0.1 ms and invert the output

*R2 = 0.1 x 10^-3/0.69 x 0.01µ = 14.492k Ω*

*R1 = (0.4 x 10^-3/0.69 x 0.01µ) - 14.492k = 43.479k Ω*

### Differentiator Circuit
Let C4 = 0.1 µF, fa = 1k Hz and fb = 10k Hz

*fa = 1/2 x pi x R4 x C4*

*R4 = 1/2 x pi x 0.1µ x 10^3 = 1.59k Ω*

*fb = 1/2 x pi x R3 x C4*

*R3 = 1/2 x pi x 0.1µ x 10 x 10^3 = 159 Ω*

### Monostable Multivibrator
*T = 1.1 x R X C*

For pulse width,T= 0.5 ms and C = 1 µF

*R = 0.5/1.1 x 10^-6 = 454.54 Ω*

### <ins>Circuit Diagram
![image](https://github.com/user-attachments/assets/a9a873cf-9096-413b-804a-2c07477ed9f8)

### 5. SIMULATION ANALYSIS
### <ins>Transient Analysis
Used to verify timing behaviour of the output signal in response to various trigger signals.

### <ins>Procedure 
1. Open LTspice and create a new schematic.Set up the circuit as per the circuit diagram.
2. Calculate the Resistor and Capacitor values for Astable block, Differentiator, clipper and Monostable block.
3. Analyse the charging and discharging of the capacitor per time.
4. Simulation Command
   - Go to **Simulate** -> *Edit Simulation Cmd*
   - Choose **Transient**, and set thime as needed per case.

### 6. OUTPUT WAVEFORMS AND RESULTS
### <ins>Case 1: 
For ton = 0.3 ms and toff = 0.2 ms, Period = 0.5 ms
### <ins>Output Waveforms

![image](https://github.com/user-attachments/assets/b1d4752c-79a3-4f35-a94f-91993c222bf2)
First waveform is the output of astable multivibrator, second waveform is the of differentiator circuit, third is the output of positive clipper circuit and lastly fourth waveform is the output of monostable multivibrator with pulse width of 0.5 ms.

**Output Result**:
  - Continuous pulse train, each 0.5 ms wide, spaced 0.5ms apart.
  - Continuous triggering causes pulses to touch or slightly overlap.

### <ins>Case 2: 
For ton = 0.7 ms and toff = 0.3 ms, Period = 1.0 ms
### <ins>Output Waveforms

![image](https://github.com/user-attachments/assets/7c47ea2d-1a10-4e8d-b2a0-c95b9db8e722)

First waveform is the output of astable multivibrator, second waveform is the of differentiator circuit, third is the output of positive clipper circuit and lastly fourth waveform is the output of monostable multivibrator with pulse width of 0.5 ms.

**Output Result**:
  - Pulse of 0.5 ms at every 1 ms.
  - The output is clean, periodic pulse:
    - **High** for 0.5 ms, then **LOW** for 0.5 ms.
  - Output duty cycle = 50%.

### <ins>Case 3: 
For ton = 0.4 ms and toff = 0.1 ms, Period = 0.5 ms. Then by using a transistor inverter, the final waveform that triggers the monostable will have 
- ton = 0.1 ms
- toff = 0.4 ms
This allows:
- Clear separation between trigger pulses.
- Enough time for the monostable to reset before the next pulse.

#### Transistor inverter circuit:

![image](https://github.com/user-attachments/assets/68467e1b-11da-4ff2-aa3f-8cb30a68d3c1)

### <ins>Output Waveforms

![image](https://github.com/user-attachments/assets/20bf1383-c7e0-41ae-8bf5-d7a9151dcd26)

First waveform is the output of inverter circuit, second waveform is the of differentiator circuit, third is the output of positive clipper circuit and lastly fourth waveform is the output of monostable multivibrator with pulse width of 0.5 ms.

**Output Result**:
  - Monostable is triggered at every 0.5 ms.
  - Monostable pulse width = 0.5 ms.
  - This results in continuous high output, as each new trigger occurs before previous monostable pulse finishes.
    
### 7. INFERENCE
- The Astable Multivibrator using a 555 timer successfully generated periodic square wave signals without requiring any external triggering.
- The **Differentiator** and **Clipper circuits** were effective in converting sqaure wave edges into narrow negative spikes, suitable for triggering monostable timer.
- The **Monostable Multivibrator** responds accurately to each valid trigger, producing consistent 0.5 ms output pulses/
- Simulation across multiple timing cases (Cases 1,2 and 3) confirms that the pulse width remains fixed at 0.5 ms, regardless of the input frequency or duty cycle.
- In **Case 3**, continuous triggering before previous pulse ends causes the monostable output to stay HIGH, demonstrating how the trigger frequency can affect pulse overlap.

### 8. CONCLUSION
The experiment demonstrates that a 555 timer can be configured in both Astable and Monostable modes to generate and shape precise timing pulse. The combination of logic elements-differentiator, clipper and inverter-ensures clean and reliable triggering of the monostable multivibrator. The system is robust, versatile and suitable for a wide range of timing applications, including waveform generation, delay circuits and digital pulse shaping.

# Virtual Lab Simulation of Monostable Multivibrator
### 1. AIM
- To perform a Monostable Multivibrator using 555 Timer
- To observe and plot the Trigger Input Voltage.
- To observe and plot the Output Voltage.
- To observe and plot the Capacitance Voltage.

### 2. PROCEDURE
1. Connect the components as mentioned below:
L1-L12, L14-L12, L16-L12, L4-L9, L8-L9, L9-L10, L3-L17, L11-L13, L7-L11, L6-L13, L5-L15.(For eg. click on 1 and then drag to 12 and so on.)
2. Click on 'Check Connection' button to check the connections.
If connected wrong, click on the wrong connection. Else click on 'Delete all connection' button to erase all the connections.
3. Intially set R a=10 kΩ, C=1 µf, Vcc=5 V, Tin = 20 msec.
4. Click on "Calculate" button.
5. Now note the output voltage.
5. Click on "Plot" button to plot, Trigger Input Voltage, Output Voltage, Capacitance Voltage
6. Click on "Clear" button to clear the data.
7. Repeat the experiment for another set of resistance value and capacitance value.
8. Set the Resistance (R a) value (1 kΩ - 10 kΩ).
9. Set the Capacitance (C) value .
10. Set supply voltage (Vcc).


### 3. CIRCUIT DIAGRAM

![Screenshot 2025-05-21 220423](https://github.com/user-attachments/assets/a4eb0e00-9dff-442b-862d-c2406f4e2ff4)

### <ins>Output Waveforms
#### Trigger Input Voltage

![image](https://github.com/user-attachments/assets/6d6ccfc7-9d76-4d5a-a3e3-14b32460d009)

#### Output Voltage

![image](https://github.com/user-attachments/assets/e31368af-5f61-45b5-84d3-05d6090ad213)

#### Capacitor Voltage

![image](https://github.com/user-attachments/assets/8bec8876-7cee-4575-aef3-9e4e60491a70)

# Virtual Lab Simulation of Astable Multivibrator
### 1. AIM
- To perform an Astable Multivibrator using 555 Timer
- To observe and plot the Output Voltage.
- To observe and plot the Capacitance Voltage.

### 2. PROCEDURE
1. Connect the components as mentioned below:
L1-L12, L14-L12, L16-L12, L4-L9, L8-L9, L10-L19, L3-L17, L11-L13, L7-L19, L6-L13, L2-L13, L5-L15, L18-L9.(For eg. click on 1 and then drag to 12 and so on.)
2. Click on 'Check Connection' button to check the connections.
If connected wrong, click on the wrong connection. Else click on 'Delete all connection' button to erase all the connections.
3. Intially set R a=3.3 kΩ, R b=6.8kΩ, C=0.1µf, Vcc=5 V.
4. Click on "Calculate" button.
5. Now note the output voltage.
6. Click on "Plot" button to plot Output Voltage, Capacitance Voltage
7. Click on "Clear" button to clear the data.
8. Repeat the experiment for another set of resistance value.
9. Set the Resistance (R a) value (1 kΩ - 10 kΩ).
10. Set the Resistance (R b) value (1 kΩ - 10 kΩ).
11. Set the Capacitance (C) value (0.1 µf - 10 µf) .
12. Set supply voltage (Vcc).

### 3. CIRCUIT DIAGRAM

![Screenshot 2025-05-21 215723](https://github.com/user-attachments/assets/634508ab-01c8-4ce9-b096-4934f8befa28)

### <ins>Output Waveforms
#### Output Voltage

![image](https://github.com/user-attachments/assets/845fba6c-71d6-47d4-bd30-719f84f3b4d6)

#### Capacitor Voltage

![image](https://github.com/user-attachments/assets/fc355c27-2f04-422e-9f73-81af28a811e2)

  







