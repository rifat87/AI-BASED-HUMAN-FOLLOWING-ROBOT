# AI-BASED-HUMAN-FOLLOWING-ROBOT

Click Here for- [Video Tutorial](https://youtu.be/UHjTWiiYeUM)

## 💡 What Does This Robot Do?

This robot can **detect a person and follow them** without any remote control. Here's the simple idea:

1. A camera on the robot watches for a person.
2. It figures out **where** the person is (left, right, or center) and **how far** away they are.
3. The robot then **turns toward** the person and **drives toward** them.
4. It keeps doing this — following the person wherever they go.
5. If something gets too close to the **back** of the robot, it stops so it doesn't crash.

---

## 🧩 The Main Parts

The robot is made up of **4 key pieces** that talk to each other:

### 1. 📷 ESP32-CAM — The Eyes
- A tiny camera module attached to the robot.
- It streams live video so a computer can see what the robot sees.

### 2. 💻 Computer / Vision System — The Brain
- A laptop or Raspberry Pi watches the camera feed.
- It detects where the person is in the frame.
- It sends two numbers to the robot: **angle** (which direction) and **distance** (how far).

### 3. 📡 ESP32 + ESP8266 — The Messengers
- These are small Wi-Fi chips.
- They wirelessly pass the angle & distance message from the computer to the robot's controller.
- Think of them as a **wireless walkie-talkie** between the brain and the body.

### 4. 🎛️ Arduino — The Body Controller
- This is the "muscle" of the robot.
- It receives the angle & distance and decides how to move.
- It controls the **wheels** (to drive forward, backward, or turn) and the **servo** (to rotate the camera).

---
## System Diagram/Architecture
<img width="1536" height="708" alt="ai-robot" src="https://github.com/user-attachments/assets/5a64452c-f0d0-4a70-bddb-5fa12aeaf26a" />


## 🔄 How It All Works — Step by Step

```
CAMERA  →  COMPUTER  →  Wi-Fi  →  ARDUINO  →  MOTORS
sees       calculates   sends      decides     move!
person     angle &      message    what        robot
           distance               to do
```

**Step 1:** The ESP32-CAM streams live video to a connected computer.

**Step 2:** The computer runs a people-detection program. It figures out:
- Is the person to the **left**, **right**, or **center**? → This becomes the **angle** (0–180°, where 90° = straight ahead).
- Is the person **close** or **far**? → This becomes the **distance** number.

**Step 3:** The computer sends those two numbers (e.g. `90,160`) to the ESP32 chip over a USB cable.

**Step 4:** The ESP32 sends that message wirelessly to the ESP8266, which passes it to the Arduino.

**Step 5:** The Arduino reads the numbers and acts:

| Situation | What the robot does |
|---|---|
| Person is straight ahead and far | Drive **forward** |
| Person is straight ahead, perfect distance | **Stop** (already in the right spot) |
| Person is straight ahead and too close | Drive **backward** |
| Person is to the **left** | Turn **left**, then adjust distance |
| Person is to the **right** | Turn **right**, then adjust distance |
| Something is behind the robot | **Stop** — won't reverse into it |

---

## 🛠️ Parts You Need

| Part | What it does |
|---|---|
| Arduino UNO | The main brain that controls movement |
| L298N Motor Driver | Lets the Arduino control the motors safely |
| 2× DC Motors + Wheels | Makes the robot move |
| Servo Motor | Rotates the camera to face the person |
| Ultrasonic Sensor (HC-SR04) | Detects obstacles behind the robot |
| ESP8266 Wi-Fi Module | Acts as a wireless receiver on the robot |
| ESP32 Wi-Fi Module | Sends messages from the computer to the robot |
| ESP32-CAM Module | Streams live video |
| Battery Pack | Powers the motors (use a separate one from the Arduino!) |
| Chassis, wires, breadboard | To put it all together |

> ⚠️ **Important:** Always power the motors from their **own battery**. Plugging motors into the Arduino's power will damage it.

---

## 🗂️ Files in This Project

| File | What it does |
|---|---|
| `Arduino Code/esp_arduino_obstacle.ino` | Controls the motors and servo |
| `ESP32 Code/esp32_as_client.ino` | Sends the angle & distance over Wi-Fi |
| `ESP8266/esp8266_as_server.ino` | Receives Wi-Fi messages and passes to Arduino |
| `ESP32 Cam module/ESP32 cam` | Runs the live camera stream |

---

## 🚀 How to Set It Up

### Step 1 — Upload code to the Arduino
1. Open **Arduino IDE**.
2. Open the file `Arduino Code/esp_arduino_obstacle.ino`.
3. Connect your Arduino via USB, select the right port, and click **Upload**.

### Step 2 — Upload code to the ESP8266
1. Open `ESP8266/esp8266_as_server.ino` in Arduino IDE.
2. Select your ESP8266 board and port.
3. Click **Upload**.

### Step 3 — Upload code to the ESP32
1. Open `ESP32 Code/esp32_as_client.ino`.
2. Select your ESP32 board and port.
3. Click **Upload**.

### Step 4 — Upload code to the ESP32-CAM *(optional)*
1. Open `ESP32 Cam module/ESP32 cam`.
2. Select **AI Thinker ESP32-CAM** as the board.
3. Upload. Once it boots, it will print a camera URL — open that in your browser to see the live feed.

---

## 🧪 Testing Without a Camera

You can test the robot without any camera or detection software. Just **type a message** into the ESP32's Serial Monitor:

| Type this | Robot should... |
|---|---|
| `90,160` | Move **forward** (centered, too far) |
| `90,150` | **Stop** (centered, perfect distance) |
| `90,130` | Move **backward** (centered, too close) |
| `60,150` | Turn **right** then stop |
| `120,160` | Turn **left** then move forward |

---

## ❓ Common Problems

**Robot doesn't move at all**
→ Check that the ESP32 and ESP8266 are connected to the same Wi-Fi. Open Serial Monitor to look for errors.

**Robot turns but won't go forward or backward**
→ Check the wiring on the L298N motor driver. Make sure the enable pins are powered.

**Arduino keeps restarting**
→ The motors are probably drawing power from the Arduino. Use a separate battery for the motors.

**Camera shows no image**
→ Make sure the camera ribbon cable is firmly connected. After flashing, reset the board with GPIO0 disconnected.

---
![image](https://github.com/Rifat87/AI-BASED-HUMAN-FOLLOWING-ROBOT/assets/102798983/afc68005-c740-4378-92da-48da00755baa)


Submitted by:
Group-01 (Team: Robo Inquisitives)


----------------------------------++++++++++++++++++---------------------------------
![IMG20230611114341](https://github.com/Rifat87/AI-BASED-HUMAN-FOLLOWING-ROBOT/assets/102798983/9c85fbd8-1386-4605-bb07-12f7d9af9adc)
----------------------------------++++++++++++++++++---------------------------------
