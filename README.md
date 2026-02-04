# Combined Pressure Meter + Scales (LabVIEW)

A LabVIEW application that **acquires and displays pressure and weight data in real time**:

- **Pressure** is acquired from **two analog input channels** using NI‑DAQmx (DAQmx API).
- **Weight** is acquired from **legacy scales over RS232** (VISA serial communication).

The program is designed to be more user-friendly than the original version it replaced, using an **event-driven layout** so you can **initialise/configure**, **start/stop acquisition**, and **save results** using dedicated buttons rather than having everything run immediately on startup.

> <img alt="Main FP" src="https://github.com/user-attachments/assets/49d248ce-038d-4276-b6bf-8144136bfb08" />


---

## What it does

- Reads **two pressure channels** from an NI DAQ device (analog voltage) and displays them live.
- Reads **weight measurements** from RS232-connected scales and displays them live.
- Provides a cleaner workflow using an **event-driven structure** (configure / acquire / save via buttons). 
- Allows saving results to a file **at any time** while running. 
- Saves files with a **timestamp-based filename** (date and time) and writes column headings automatically.

---

## Typical use case

Originally created for a setup used in **Chemical Engineering**, combining a pressure measurement system with older RS232 scales hardware. This project also serves as a useful example of combining **NI‑DAQmx acquisition** and **VISA serial acquisition** in a single application.

---

## Requirements

- **LabVIEW 2021** (developed in LabVIEW 2021).
- **NI‑DAQmx drivers** installed (for NI DAQ acquisition).
- A compatible **NI DAQ device** with at least 2 analog input channels.
- RS232-capable scales (or RS232 → USB adapter) and access to the correct COM port for VISA.  

---

## How to run

1. Open the LabVIEW project:
   - `Combined Pressure Meter Scales.lvproj`
2. Open the main VI:
   - `main.vi`
3. Click the **Run** arrow in LabVIEW.

---

## How to use (simple workflow)

### 1) Initialise / configure hardware
Click **Initialise** to open the configuration dialog.  
This lets you set both:
- **NI DAQ settings** (pressure channels), and
- **VISA serial settings** (scales). 

Configuration is stored in two type-definition clusters used throughout the program:
- `ConfigNI` (DAQ settings)
- `ConfigVISA` (serial settings) 

### 2) Start acquisition
Once initialised, start the acquisition to display:
- Pressure channel 1
- Pressure channel 2
- Scales reading (weight)  
all updating in real time. 

### 3) Save results (any time)
Use the save button to create a results file and begin writing data.  
Files are created with an automatic **date/time filename**, include headings, and data is written in a simple row format including:
- Time (timestamp string)
- Mean pressure values (from the live data)
- Scales value

### 4) Stop and close
Stop acquisition before closing the program to ensure devices/ports and files are closed cleanly.

---

## Project structure (what’s in this repo)

Key files and folders you’ll see in the repository include:

- `main.vi` — main application VI
- `Combined Pressure Meter Scales.lvproj` — LabVIEW project file
- `ConfigNI.ctl` — NI DAQ configuration typedef
- `ConfigVISA.ctl` — VISA serial configuration typedef 
- `DAQ_class/` — class handling DAQmx + VISA acquisition logic 
- `File_class/` — class handling file creation/writing/closing 
- `Pressure Scales.uml` — UML diagram used to plan the class design 

---

## Troubleshooting

**No pressure data**
- Confirm NI‑DAQmx is installed and the NI DAQ device is connected. 
- Re-check the NI configuration in the Initialise dialog.

**No scales reading**
- Confirm the correct COM port is selected and the scales are connected via RS232/USB. 
- Re-check VISA configuration (including the command/write buffer and delay before read).

**File not saving / empty file**
- Ensure you have pressed the save/create file action and that the program is running long enough to log data. 

---

## Support / contact

For support or to adapt this program for a different pressure/scales setup, contact the  
**Electronics & Software Labs** team.
