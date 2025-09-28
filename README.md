# smart-irrigation-system
ojectives:

What it does:
This project automatically waters plants based on soil moisture levels. A soil moisture sensor reads the water content in the soil, and when it drops below a set threshold, the Arduino activates a water pump to irrigate the plants.

Why I chose it:
I selected this project because agriculture and gardening require efficient water use. Automating irrigation saves time, reduces water wastage, and ensures healthy plant growth.
It also demonstrates how IoT and automation can solve real-life problems.

block diagram:
<img width="413" height="217" alt="image" src="https://github.com/user-attachments/assets/444234c7-786e-42a6-93b6-21722bf4e0cc" />

omponents Used in
 Tinkercad):
- Arduino Uno
- Breadboard
- Sensor/Actuators (e.g., Soil Moisture Sensor,DC motor )
- Resistor
- Jumper Wires
- NPN transistor with diode

- Circuit Diagram
![Circuit Diagram]

<img width="993" height="752" alt="Screenshot 2025-09-28 133710" src="https://github.com/user-attachments/assets/390b9094-3085-4f6a-a3ad-4d1a84fee46d" />

<img width="798" height="697" alt="Screenshot 2025-09-28 131506" src="https://github.com/user-attachments/assets/00d2fa4f-13e8-4613-8a24-43cb08d0491f" />


Arduino Code

#include <Wire.h>
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(32, 16, 2);  

int sensorPin = A0;
int motorPin = 9;       
int sensorValue = 0;
int threshold = 500;    
void setup() {
  pinMode(motorPin, OUTPUT);
  lcd.init();
  lcd.backlight();
  lcd.setCursor(0,1);
  lcd.print("Smart Irrigation");
  delay(2000);
  lcd.clear();
}

void loop() {
  sensorValue = analogRead(sensorPin);

  lcd.setCursor(0,0);
  lcd.print("Soil Value:");
  lcd.print(sensorValue);

  if(sensorValue < threshold) {
    digitalWrite(motorPin, HIGH);  
    lcd.setCursor(0,1);
    lcd.print("Watering");
  } else {
    digitalWrite(motorPin, LOW);   // Pump OFF
    lcd.setCursor(0,1);
    lcd.print(" Moist      ");
  }

  delay(1000);
}


