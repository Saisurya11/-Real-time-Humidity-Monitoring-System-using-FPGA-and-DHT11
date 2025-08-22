<img width="1024" height="411" alt="image" src="https://github.com/user-attachments/assets/55936265-b7c6-4c4a-9a5d-eac0f1df00ca" /># FPGA-Based Humidity Monitoring & Control System  
*Using DHT11 Sensor + Nexys 4 DDR (Artix-7 FPGA)*  

---

## 📖 Project Overview  
This project demonstrates how to interface the **DHT11 humidity & temperature sensor** with an **FPGA** and use it to build a **real-time monitoring and control system**.  

Unlike microcontrollers, FPGA requires precise logic design to manage the **1 µs timing-sensitive protocol** of the DHT11. The system was implemented on the **Nexys 4 DDR (Artix-7)** board using **Verilog HDL**.  

---

## ✨ Features  
- **DHT11 Interfacing with FPGA** (1 µs precision)  
- **Checksum verification** for reliable data  
- **Seven-Segment Display** output for humidity/temperature  
- **Motor Control** when humidity < threshold  
- **LED Error Indicators** for debugging and fault detection  

---

## ⚙️ Hardware & Tools  
- **Board:** Nexys 4 DDR (Xilinx Artix-7 FPGA)  
- **Sensor:** DHT11 (Temperature & Humidity)  
- **Display:** Onboard Seven-Segment LEDs  
- **Tools:** Verilog HDL, Xilinx Vivado  

---

## 🔄 DHT11 Communication Protocol  

The DHT11 sensor uses a **single-wire bidirectional protocol** with strict timing requirements.  

1. **Start Signal (Host → Sensor):**  
   - Host (FPGA) pulls data line **low for at least 18 ms** to request data.  
   - Host then releases the line and waits.  

2. **Response Signal (Sensor → Host):**  
   - Sensor pulls the line **low for 80 µs**, then **high for 80 µs**, confirming readiness.  

3. **Data Transmission (40 Bits):**  
   - Sensor sends **40 bits** in the form:  
     - 8-bit Humidity integer  
     - 8-bit Humidity decimal  
     - 8-bit Temperature integer  
     - 8-bit Temperature decimal  
     - 8-bit Checksum (for error validation)  
   - Each bit has:  
     - **50 µs LOW** start  
     - Followed by **26–28 µs HIGH = "0"**, or **70 µs HIGH = "1"**  

4. **Checksum Verification:**  
   - The last 8 bits are a checksum.  
   - Sum of first 4 bytes must match the checksum for data to be valid.  

---

## 📷 Protocol Diagram (DHT22 Reference)  
Although DHT11 and DHT22 differ slightly in resolution, both follow the same **pulse-width encoding method**:  
<img width="1500" height="325" alt="2_DHT11_Frame" src="https://github.com/user-attachments/assets/8beb0ff2-733a-42dc-a2ad-655e4b71826a" />


---

## 📂 Repository Contents  
/OUTPUT — Captures of seven-segment outputs
/dht.txt — Verilog source code
/dht_xdc.txt — FPGA pin constraints (Vivado)
README.md — Project documentation


---

## 🔮 Future Enhancements  
- Upgrade to **DHT22** for better accuracy  
- Add **UART/serial logging** to PC  
- Extend to **IoT/cloud integration**  

---

## 📌 Key Learnings  
- Handling **timing-sensitive sensor protocols** in FPGA  
- Designing **state machines** in Verilog  
- Implementing **real-time control systems** entirely on hardware  
- Debugging using LEDs and checksum logic  

---
