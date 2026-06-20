# IoT Smart Home Automation using ESP32 and Blynk

A professional-grade Internet of Things (IoT) home automation system designed to control household appliances (simulated via AC light bulbs) remotely through a smartphone. The system leverages an ESP32 microcontroller, a multi-channel mechanical relay isolation module, and the Blynk IoT cloud platform for secure, real-time wireless control over Wi-Fi.

---

## 📌 Project Architecture & Flow

```text
[Mobile Phone (Blynk App)] ──(Wi-Fi / Blynk Cloud)──> [ESP32 Microcontroller]
                                                        │
                                           (Low-Voltage GPIO Signal)
                                                        │
                                                        ▼
[Dual AC Power Sources] <───(High-Voltage Switching)─── [2-Channel Relay Module]
            │                                                    │
            └───────────────────> [2x Light Bulbs] <─────────────┘
```

1. **User Interface:** The user toggles digital switches on the Blynk mobile app interface.
2. **Cloud Orchestration:** Commands are sent securely over the internet via WebSockets to the Blynk IoT Cloud Server.
3. **Edge Processing:** The ESP32, maintaining a persistent Wi-Fi connection to Blynk, receives the downstream state changes.
4. **Hardware Isolation:** The ESP32 manipulates low-voltage GPIO pins to switch optocoupler-isolated mechanical relays.
5. **Actuation:** The relays open or close the 230V/110V AC electrical circuit paths, toggling the light bulbs instantly.

---

## 🛠️ Hardware Requirements & Bill of Materials (BOM)

| Component                                | Description                                                    | Quantity |
| ---------------------------------------- | -------------------------------------------------------------- | -------- |
| **ESP32 NodeMCU Development Board**      | Main dual-core microcontroller with integrated Wi-Fi stack.    | 1        |
| **2-Channel 5V Relay Module**            | Optocoupler-isolated mechanical switches rating 10A @ 250VAC.  | 1        |
| **AC Light Bulbs & Holders**             | Targeted household appliance loads.                            | 2        |
| **Solderless Breadboard & Jumper Wires** | Prototyping infrastructure.                                    | 1        |
| **External Power Supplies**              | Separate mains/AC lines for load, USB 5V for microcontrollers. | 2        |

---

## 🔌 Circuit Connections

### 1. Low-Voltage Logic Side

* **ESP32 GND** → **Relay GND** (Common Ground Reference)
* **ESP32 5V / Vin** → **Relay VCC** (5V power to energize relay coils)
* **ESP32 GPIO Pin (e.g., D18)** → **Relay IN1** (Controls Channel 1)
* **ESP32 GPIO Pin (e.g., D19)** → **Relay IN2** (Controls Channel 2)

### 2. High-Voltage Load Side (AC Mains)

* **AC Mains Phase/Live (+)** → Wired directly to one terminal of the **Bulb**
* **AC Mains Neutral/Negative (-)** → Connected to the Relay **Normally Open (NO)** terminal
* **Relay Common (COM)** → Connected to the remaining terminal of the **Bulb**


### Prerequisites

1. Install the latest version of the Arduino IDE.
2. Add ESP32 Core Support via **Boards Manager**.
3. Install the **Blynk** library via:

   ```
   Sketch → Include Library → Manage Libraries
   ```

### Firmware Installation

1. Clone this repository to your local machine.

2. Open the project file in Arduino IDE.

3. Update the Template ID, Auth Token, and Wi-Fi credentials.

4. Select your ESP32 board under:

   ```
   Tools → Board
   ```

5. Connect the ESP32 using USB.

6. Select the correct COM Port.

7. Click **Upload**.

---

## 📱 Mobile App Configurations (Blynk)

### Step 1: Create Template

* Log in to the Blynk IoT dashboard.
* Create a new template named **Smart Home**.

### Step 2: Configure Datastreams

| Virtual Pin | Type    | Range | Purpose               |
| ----------- | ------- | ----- | --------------------- |
| V1          | Integer | 0–1   | Controls Light Bulb 1 |
| V2          | Integer | 0–1   | Controls Light Bulb 2 |

### Step 3: Design Dashboard

1. Open the Blynk Mobile App.
2. Add two **Button Widgets**.
3. Set both buttons to **Switch Mode**.
4. Assign:

   * Button 1 → V1
   * Button 2 → V2

---

## 🔒 Safety Precautions

* Always disconnect mains power before wiring the circuit.
* Use insulated wires and properly rated relay modules.
* Never touch exposed AC terminals while the system is powered.
* Verify all connections with a multimeter before energizing the circuit.
* Consider using fuse protection for additional safety.

---

## 🚀 Future Enhancements

* Voice control using Google Assistant or Alexa.
* Energy consumption monitoring.
* Scheduling and automation routines.
* Sensor integration (temperature, motion, gas leakage).
* Local web dashboard for offline operation.
* MQTT-based communication architecture.

---

## 📸 Project Demonstration

### Features

* Remote control of appliances using smartphone.
* Real-time cloud synchronization.
* Wi-Fi connectivity via ESP32.
* Electrical isolation using relay modules.
* Scalable architecture for additional devices.


This project is licensed under the MIT License. See the `LICENSE` file for details.
