# Industrial OT/IT Integration: PLC & Python OPC UA Data Logging & Telemetry System

## 📌 Project Overview
This project demonstrates a production-grade, reliable OT/IT integration pipeline. It establishes a secure, asynchronous data-logging interface between 
a Siemens S7 PLC (S7-1200 / S7-1500) and a Python supervisory environment using the **OPC UA protocol**.

---

## 🔍 The Problem & The Solution
* **The Challenge:** Modern industrial automation often faces the hurdle of bridging field-level control (OT) with higher-level IT environments.
* Relying on complex, heavy AI models at the edge introduces unnecessary points of failure, unpredictability, and latency in mission-critical applications.

* **The Solution:** We deliberately shifted away from volatile AI implementations toward a robust, deterministic, rule-based monitoring and logging architecture.
  Core control and safety logic remain strictly inside the PLC (written in SCL) for real-time determinism, while Python acts as a dedicated supervisory layer
  for reliable telemetry extraction.

---

## 📊 Motor State Documentation & Research Value
This system acts as a comprehensive historical telemetry documentation tool for industrial assets:
* **Continuous Telemetry Tracking:** Automatically records timestamped operational states, including rotational speed (`Speed`) and thermal behavior (`Temp`).
* **Environmental & Seasonal Impact Analysis:** By maintaining a structured, long-term CSV log, this repository serves as a research foundation. It enables
* engineers to analyze how external factors, seasonal temperature shifts, or specific times of day correlate with motor thermal performance and efficiency over time.

---

## 🛡️ Safety & Engineering Architecture
* **Strict Control Separation:** Safety-critical tasks and fast execution loops are handled deterministically within the PLC, ensuring absolute independence
* from external software.
* **Non-Blocking IT Layer:** The Python supervisory script utilizes asynchronous programming (`asyncua`), guaranteeing that any network glitch, file-locking issue,
* or software restart in the IT layer will never compromise the physical safety or operation of the industrial machine.

---

## 🏗️ System Architecture
1. **OT Layer (Siemens TIA Portal):** S7 PLC running a cyclic interrupt (`OB30`) to simulate realistic motor dynamics, exposing designated tags via a native OPC UA
   Server interface (`Motor_Data` DB).
2. **Communication Protocol:** Industrial standard OPC UA over TCP (`asyncua` client library).
3. **IT Layer (Python Supervisory):** Asynchronous telemetry ingestion and structured CSV data archiving.

---

## 🚀 How to Run
1. Ensure your Siemens PLC or TIA Portal Simulation is running with the OPC UA Server enabled.
2. Clone the repository and install the required dependencies:
   ```bash
   pip install asyncua
   Update the PLC_URL and node addresses in Client.py to match your local network configuration.

Run the script:

Bash
python Client.py
