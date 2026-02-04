# TrafficXia — Adaptive Traffic Signal Using Computer Vision

TrafficXia is a real-time traffic signal controller that dynamically adjusts signal timings using live camera feeds instead of fixed schedules.

It is designed for dense and mixed traffic environments (common in urban roads) where traditional signals waste green time and fail to react to congestion.

> Current version focuses on vehicle-based adaptive control. Emergency vehicle prioritization is planned in future releases.

---

## Overview
TrafficXia behaves like a responsive intersection controller rather than a static timer.  
It observes traffic using cameras, estimates lane demand, and allocates signal time accordingly.

---

## Features
- Supports **2–4 approaches** (each mapped to a camera feed)
- Real-time vehicle detection using **YOLO**
- Counts vehicles per approach (pedestrians ignored)
- Adaptive signal timing:
  - GREEN starts with a base duration
  - Extends if vehicles continue arriving
  - Terminates early when lane is empty
- Safe transitions: **GREEN → YELLOW → ALL-RED → next GREEN**
- Startup configuration UI for mapping cameras to approaches
- Fair rotation across approaches

---

## System Pipeline
Camera Feed → Vehicle Detection → Vehicle Count → Decision Logic → Signal State

---

## Behaviour Flow
1. Opens camera feeds
2. Detects and counts vehicles per approach
3. Allocates GREEN to one approach at a time
4. Skips empty lanes quickly
5. Extends GREEN for continuous flow
6. Rotates fairly across approaches

---

## Motivation
Fixed-time traffic signals perform poorly when:
- traffic density changes frequently
- lanes are unstructured
- vehicle types vary (bike/auto/bus/truck)
- immediate response is required

TrafficXia adapts signal timing in real-time instead of relying on preset timing plans.

---

## Current Limitations
- Detection accuracy depends on camera placement and lighting
- Heavy congestion may require ROI tuning
- Prototype supports a single intersection

---

## Planned Improvements
- Emergency vehicle prioritization (siren/GPS/V2X)
- Multi-intersection coordination (green wave)
- Weather/time-aware policies
- Distributed intersections via MQTT/WebSockets
- Hardware signal interface (Arduino/ESP32/PLC)
- Monitoring dashboard and logging

---

## Requirements
- Python 3.10+
- ultralytics
- opencv-python
- numpy
- sounddevice
- librosa
- tensorflow

---

## Installation
```bash
pip install -r requirements.txt
```

## Run
```bash
python main.py
```

---

## License
GNU Affero General Public License v3.0 (AGPL-3.0)

This project uses Ultralytics YOLO models which follow the same license.  
Commercial usage may require a commercial license from Ultralytics.
