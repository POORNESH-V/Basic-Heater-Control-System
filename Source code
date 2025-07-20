#include <OneWire.h>
#include <DallasTemperature.h>

// Pin def
#define ONE_WIRE_BUS 2       // DS18B20 data pin
#define HEATER_PIN 7         // Heater LED
#define BUZZER_PIN 8         // Buzzer pin

// Temp Sensor Setup
OneWire oneWire(ONE_WIRE_BUS);
DallasTemperature sensors(&oneWire);

// Timing Variables
unsigned long lastReadTime = 0;
const unsigned long interval = 1000;  // 1s

// Threshold 
const float idleLimit = 30.0;
const float stabilizingLow = 55.0;
const float targetTemp = 60.0;
const float overheatTemp = 80.0;

// Enum to represent heater states
enum HeaterState {
  IDLE,
  HEATING,
  STABILIZING,
  TARGET_REACHED,
  OVERHEAT
};

HeaterState currentState = IDLE;

void setup() {
  Serial.begin(9600);
  sensors.begin();
  pinMode(HEATER_PIN, OUTPUT);
  pinMode(BUZZER_PIN, OUTPUT);
  digitalWrite(HEATER_PIN, LOW);
  digitalWrite(BUZZER_PIN, LOW);
}

void loop() {
  unsigned long currentTime = millis();

  // Non-blocking read every 1 second
  if (currentTime - lastReadTime >= interval) {
    lastReadTime = currentTime;

    // Read temperature
    sensors.requestTemperatures();
    float temperature = sensors.getTempCByIndex(0);

    // Determine state
    if (temperature >= overheatTemp) {
      currentState = OVERHEAT;
    } else if (temperature >= targetTemp) {
      currentState = TARGET_REACHED;
    } else if (temperature >= stabilizingLow) {
      currentState = STABILIZING;
    } else if (temperature > idleLimit) {
      currentState = HEATING;
    } else {
      currentState = IDLE;
    }

    // React based on state
    switch (currentState) {
      case IDLE:
        digitalWrite(HEATER_PIN, LOW);
        digitalWrite(BUZZER_PIN, LOW);
        Serial.print("State: IDLE | ");
        break;

      case HEATING:
        digitalWrite(HEATER_PIN, HIGH);
        digitalWrite(BUZZER_PIN, LOW);
        Serial.print("State: HEATING | ");
        break;

      case STABILIZING:
        digitalWrite(HEATER_PIN, HIGH);
        digitalWrite(BUZZER_PIN, LOW);
        Serial.print("State: STABILIZING | ");
        break;

      case TARGET_REACHED:
        digitalWrite(HEATER_PIN, LOW);
        digitalWrite(BUZZER_PIN, LOW);
        Serial.print("State: TARGET REACHED | ");
        break;

      case OVERHEAT:
        digitalWrite(HEATER_PIN, LOW);
        digitalWrite(BUZZER_PIN, HIGH); // Buzzer ON
        Serial.print("State: OVERHEAT! | ");
        break;
    }

    // Serial output with temperature
    Serial.print("Temperature: ");
    Serial.print(temperature);
    Serial.println(" °C");
  }
}
