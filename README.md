# smart-fan-control
Tinkercad design for smart fan control using ARDUINO UNO and TMP36 sensors 
// Smart Fan Control Using TMP36 and Arduino
// Author: Vinoth Kumar M.S

const int tempPin = A0;     // TMP36 sensor connected to A0
const int fanPin = 9;       // Fan (via transistor) connected to D9
const float threshold = 35; // Temperature in °C to turn ON fan

void setup() {
  pinMode(fanPin, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  int sensorValue = analogRead(tempPin);
  
  // Convert analog value (0-1023) to voltage (0-5V)
  float voltage = sensorValue * (5.0 / 1023.0);

  // Convert voltage to temperature in Celsius
  float temperature = (voltage - 0.5) * 100;

  // Debugging output
  Serial.print("Temperature: ");
  Serial.print(temperature);
  Serial.println(" °C");

  // Fan control logic
  if (temperature >= threshold) {
    digitalWrite(fanPin, HIGH); // Turn ON fan
  } else {
    digitalWrite(fanPin, LOW);  // Turn OFF fan
  }

  delay(1000); // Wait 1 second
}

