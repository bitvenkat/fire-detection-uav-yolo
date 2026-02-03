# fire-detection-uav-yolo

📖 Overview
Forest fires cause massive ecological damage, and satellite systems often fail to detect them early enough. This project proposes a low-cost, autonomous UAV system that utilizes Edge AI to detect fire in real-time without relying on cloud connectivity.

This research demonstrates a custom-built Quadcopter integrated with a Raspberry Pi 4 and YOLOv11n to achieve high-accuracy detection (mAP 93.6%) suitable for embedded deployment.

Note: This project is associated with the research paper "A Lightweight Fire Detection Framework Based on YOLOv11 for Deployment on Embedded UAV Systems" (currently under review).

⚙️ Tech Stack & Hardware
This project bridges Deep Learning and IoT/Robotics.

AI Model: YOLOv11n (Nano) optimized for edge devices.

Edge Computing: Raspberry Pi 4 (4GB).

Flight Controller: Custom Arduino-based flight controller (YMFC-AL design) + MPU6050 Gyro/Accel.

Connectivity: FlySky RC communication (with planned mobile telemetry).

Language: Python (Inference), C++ (Arduino).

🏗️ System Architecture
The system consists of a custom-built drone frame utilizing a distributed processing architecture:

Flight Control: Arduino Uno handles stability (PID loops) and motor control.

Vision Processing: Raspberry Pi 4 captures video, runs the YOLOv11 inference, and flags fire events.


📊 Performance & Results
The model was trained on a dataset of 3426 images and tested against real-world video footage.

mAP (0.5): 93.6%

Precision: 93.0%

Inference Speed: ~8 FPS on Raspberry Pi 4 (CPU only)

Accuracy: 92% on video test set.



🚀 Installation & Usage
1. Hardware Requirements

Raspberry Pi 4 Model B

Pi Camera Module V2

Custom Drone Frame (F450 or similar)

2. Setup

# Clone the repository
git clone https://github.com/bitvenkat/fire-detection-uav-yolo.git

# Install dependencies
pip install -r requirements.txt

# Run Inference on RPi
python src/inference/detect_fire.py --source 0 --weights models/yolov11n_fire.pt


🔮 Future Roadmap (Mobile Integration)
To enhance the system for commercial deployment, the following features are in development:

Flutter Mobile App: A cross-platform Ground Control Station (GCS) app to receive real-time alerts from the drone via MQTT/LoRa.

GPS Waypoints: Autonomous path planning integration.

👨‍💻 Author
Venkat Bhardwaj
Researcher, School of Engineering, JNU


📱 Proposed Mobile Integration (Flutter + IoT Architecture)

To translate the drone's edge detection into actionable intelligence for ground teams, a cross-platform mobile application is designed using Flutter. This architecture bridges the YOLOv11 inference engine  with a user-friendly frontend via standard IoT protocols.

1. System Data Flow

The system follows a Publisher/Subscriber model to ensure low-latency alerts:
graph TD


    A[Drone/RPi 4] -- "1. Fire Detected (YOLOv11)" --> B(Edge Processing)
    B -- "2. Publish JSON Payload (MQTT/4G)" --> C{Cloud Broker / Firebase}
    C -- "3. Push Notification" --> D[Flutter Mobile App]
    D -- "4. Live Location & Feed" --> E[User Interface]



2. Technical Implementation Plan
  
The Raspberry Pi 4, acting as the IoT Edge device, runs a Python script that triggers a callback when conf > 0.5. This triggers an MQTT publish event.

1. Edge-Side Payload (Python)

When the YOLOv11n model detects fire, the RPi transmits a lightweight JSON packet to minimize bandwidth usage in remote areas:

2. App-Side Handling (Flutter/Dart)

The Flutter application utilizes the mqtt_client package to listen for critical alerts.

3. **Why Flutter?**

Single Codebase: Deploys to both Android (for field rangers) and iOS (for command centers).

Google Maps Integration: Renders the drone's flight path and fire coordinates on a satellite layer.

Performance: Handles high-frequency telemetry updates (60fps) required for tracking a drone moving at speed.

## 📜 Citation
If you use this code or dataset in your research, please cite the associated paper (currently under review):


```bibtex
@article{bhardwaj2026fire,
  title={A Lightweight Fire Detection Framework Based on YOLOv11 for Deployment on Embedded UAV Systems},
  author={Bhardwaj, Venkat and Akanksha and Devi, G. Renuka},
  journal={Preprint submitted to Elsevier},
  year={2026}
}


