# ESP8266: Program (with ESP32-CAM-MB or without)

Step-by-step guide to programming an ESP8266 using an **ESP32-CAM-MB board programmer** or another USB-to-serial programmer.

**Author:** Eva Mateev  
**License:** CC BY 4.0

---

## Connect ESP8266 to ESP32-CAM-MB Programmer

The ESP8266 can be programmed using an **ESP32-CAM-MB board programmer**. The programmer provides the USB-to-serial connection needed to upload firmware to the ESP8266.

> **Note:** You can program the ESP8266 with any USB-to-serial programmer. Simply follow the pinout and programming instructions below, excluding the ESP32-CAM-MB specific wiring modifications.

Use the ESP8266 pinout to correctly identify and connect each pin to the ESP32-CAM-MB programmer.

| **ESP8266** | **ESP32-CAM-MB** | **Notes**                                         |
| ----------- | ---------------- | ------------------------------------------------- |
| RST         | RST              | Reset connection                                  |
| VCC         | 3.3V             | **3.3V ONLY** — do not connect to 5V              |
| EN          | 3.3V             | Can be connected directly to VCC when VCC is 3.3V |
| IO0         | IO0              | Must be held LOW to enter programming mode        |
| IO15        | GND              | Must be LOW to boot correctly                     |
| TX          | RX               | ESP8266 TX → programmer RX                        |
| RX          | TX               | ESP8266 RX → programmer TX                        |

---

## Programming Mode

The **IO0 pin must be held LOW** when the ESP8266 is reset in order to enter programming mode.

1. Connect **IO15 directly to GND**. IO15 must remain LOW for the ESP8266 to boot correctly.
2. Connect **EN to 3.3V**. EN can simply be connected to VCC when VCC is connected to 3.3V.
3. **TX and RX must be crossed:** ESP8266 TX -> programmer RX, and ESP8266 RX -> programmed TX.
4. Connect **IO0 to IO0** on the ESP32-CAM-MB programmer.
5. Hold **IO0 LOW**.
6. Click the **RST/Reset** button.
7. Continue clicking Reset until the Serial Monitor shows a boot message beginning with approximately:

   * `(1,6)` or
   * `(1,7)`
8. You should normally only need to press Reset **1–3 times**.
9. Once the ESP8266 has entered programming mode, **release IO0**.
10. Upload the firmware using the Arduino IDE.

---

## Important Notes

* **VCC must be 3.3V. The ESP8266 is a 3.3V-only device. Do not connect VCC to 5V.**
* **EN must be HIGH (3.3V) for the ESP8266 to operate.** Connecting EN directly to VCC is acceptable when VCC is connected to 3.3V.
* **IO0 must be LOW during reset** to enter programming/flash mode.
* **IO15 must be connected directly to GND** because it must be LOW for the ESP8266 to boot correctly.
* **TX and RX must be crossed:** ESP8266 TX → programmer RX, and ESP8266 RX → programmer TX.
* Refer to the project's wiring diagram/pinout before making the connections.
* Once programming mode has been entered, **IO0 can be released**.

---

## ESP32-CAM-MB Wiring Modifications

The ESP32-CAM-MB board has some important wiring connections that need to be made when using it as a programmer.

### GND Connection

The **GND pin on the right-hand side of the ESP32-CAM-MB is NC (Not Connected)**.

Because of this, you must connect the **GND connection on the left-hand side, underneath +5V, to the other GND pin** on the ESP32-CAM-MB.

> **Important:** Do not assume that the right-hand-side GND connection is electrically connected. Use the functional GND connection shown in the wiring diagram.

### 6206A A403/33 3.3V Voltage Regulator

The **6206A A403/33** is a low-dropout (LDO) **3.3V voltage regulator IC** used with the ESP32-CAM-MB.

The **3rd leg of the 6206A A403/33** needs to be connected to the **3.3V connection on the right-hand side of the ESP32-CAM-MB**.

The right-hand-side 3.3V connection pin is otherwise **NC**, so this connection must be made according to the project's wiring diagram.

> **Refer to the wiring diagram for the correct physical connection and orientation of the 6206A A403/33.**

---

## ESP32-CAM-MB Pinout and Wiring Modifications

![ESP32-CAM-MB Pinout](ESP32-CAM-MB%20Pinout.png)

---

## License

This project is licensed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)** license.

You are free to share and adapt this work, provided that appropriate credit is given to the original author.

**Author:** Eva Mateev  
**License:** CC BY 4.0
