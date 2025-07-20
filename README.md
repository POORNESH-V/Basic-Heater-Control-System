# Basic Heater Control System – upliance.ai Assignment

This project is a simulation of a temperature-based heater control system, designed as part of the Embedded Systems Internship assignment for upliance.ai. It demonstrates state tracking, temperature-based actuation, and visual/audible feedback using basic components.

---

## Features

✅ Continuously reads temperature using DS18B20 sensor  
✅ Controls a simulated heater (LED) based on temperature thresholds  
✅ Tracks and logs system states:  
- `IDLE`: Temp < 30°C  
- `HEATING`: 30°C ≤ Temp < 55°C  
- `STABILIZING`: 55°C ≤ Temp < 60°C  
- `TARGET_REACHED`: 60°C ≤ Temp < 80°C  
- `OVERHEAT`: Temp ≥ 80°C  
✅ Buzzer alerts during overheat  
✅ Logs system state and temperature to Serial Monitor  
✅ Uses non-blocking timing (`millis()`) instead of `delay()`  

---

## Components Used (in Wokwi)

- Arduino Uno  
- DS18B20 temperature sensor  
- 4.7kΩ pull-up resistor (between VCC and DQ of DS18B20)  
- Heater LED (connected to D7)  
- 220Ω resistor (LED current limiting)  
- Buzzer (connected to D8)

---

## Circuit Overview

**DS18B20 Wiring:**

| DS18B20 Pin | Arduino Pin |
|-------------|-------------|
| GND         | GND         |
| VCC         | 5V          |
| DQ          | D2 + 4.7kΩ pull-up to VCC |

**Heater Simulation:**
- D7 → LED → 220Ω → GND

**Buzzer:**
- D8 → Buzzer +  
- Buzzer – → GND

---

## How to test this?

1. Open the project in Wokwi.  LINK:([https://wokwi.com/](https://wokwi.com/projects/436737721879823361))
2. Simulate the circuit drawn
3. Click the DS18B20 sensor to change the temperature status
4. Observe the LED and buzzer behavior
5. Open the Serial Monitor to see live logs

---

## Circuit diagram (Architecture)

<img width="794" height="648" alt="image" src="https://github.com/user-attachments/assets/836218e0-eb45-459e-8857-508cd894634c" />


---

## Project Status

1. Core functionality implemented  
2. Bonus feature: Buzzer feedback  
3. FreeRTOS and BLE not implemented (optional scope)




