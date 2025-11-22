---
sidebar_position: 2
---

# Day 1 Projects
# 第1天项目

## Morning: Spaghetti Marshmallow Challenge
## 上午：Spaghetti Marshmallow 挑战

### Challenge Results | 挑战结果

- **Team Name | 团队名称**: The Spaghetti Squad
- **Final Height | 最终高度**: 45 cm
- **Marshmallow on Top? | 棉花糖在顶部？**: Yes

### Our Approach | 我们的方法

Our initial plan was to build a wide triangular base for stability, then create a central tower with diagonal support for maximum height. 

### What We Learned | 我们学到了什么

1. Short supports/spagettis are more stable and strong
2. Triangle is indeed a very strong structure
3. Team work division is important.

### Photos | 照片

N/A

---

## Afternoon: Arduino Hardware CTF
## 下午：Arduino 硬件 CTF

### Flags Captured | 捕获的 Flag

- [x] Flag 1: Sensor Reading
- [ ] Flag 2: Actuator Control
- [ ] Flag 3: Sensor to Actuator
- [ ] Flag 4: Complex Logic
- [x] Flag 5: Creative Project

### My Favorite Challenge | 我最喜欢的挑战

**Which flag was most interesting? | 哪个 flag 最有趣？**

I did Arduino Tutorial 19 "Gesture-Controlled Light". It was a simple logic, but very interesting to interact.

### Arduino Code Snippet | Arduino 代码片段

Here's a code snippet from one of my challenges:

这是我某个挑战中的代码片段：

```cpp
// Add your Arduino code here
// 在这里添加你的 Arduino 代码
	int ledPin = 13;       // Define the LED pin 13
int lightSensor1 = 0;  // Define the left light sensor pin A0
int lightSensor2 = 1;  // Define the right light sensor pin A1
 
int cali1 = 0;         // Calibration variable for left light sensor
int cali2 = 0;         // Calibration variable for right light sensor
 
bool isOn = false;     // LED state control variable
 
void setup() {
  Serial.begin(9600);       // Initialize serial communication
  
  pinMode(ledPin, OUTPUT);  // Set the LED pin as output
 
  /*Calibrate light sensors: read data 10 times and average as ambient light baseline*/
  for (int i = 0; i < 10; i++) {
    cali1 += analogRead(lightSensor1);
    cali2 += analogRead(lightSensor2);
    delay(500);
  }
  cali1 = (cali1 / 10);
  cali2 = (cali2 / 10);
 
  Serial.print("Ambient light: ");
  Serial.print(cali1);
  Serial.print(" , ");
  Serial.println(cali2);
 
  // Blink the LED twice to indicate the start of the program
  for (int i = 0; i < 2; i++) {
    digitalWrite(ledPin, HIGH);
    delay(1000);
    digitalWrite(ledPin, LOW);
    delay(1000);
  }
 
  Serial.println("Start");
}
 
void loop() {
  int sensorVal1 = analogRead(lightSensor1);  
// Read the value of the left light sensor
  int sensorVal2 = analogRead(lightSensor2);  
// Read the value of the right light sensor
 
  int threshold = 30;  
// Set the threshold value for gesture detection
 
  Serial.print("L: ");
  Serial.print(sensorVal1);
  Serial.print("   R: ");
  Serial.println(sensorVal2);
 
  // Determine gesture direction and control the LED
  if ((sensorVal1 > (cali1 + threshold)) && !(sensorVal2 > (cali2 + threshold))) {
    isOn = true;
  }
 
  if (!(sensorVal1 > (cali1 + threshold)) && (sensorVal2 > (cali2 + threshold))) {
    isOn = false;
  }
 
  if (isOn) {
    digitalWrite(ledPin, HIGH);  // Turn on the LED
    Serial.println("Turn On");
  } else {
    digitalWrite(ledPin, LOW);   // Turn off the LED
    Serial.println("Turn Off");
  }
 
  delay(100);  // Delay 100 milliseconds to avoid frequent readings
}