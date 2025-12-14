# 👁️ YOLO Object Detection & Tracking Projects

This repository contains a collection of computer vision projects utilizing **YOLOv8** (You Only Look Once) for real-time object detection and **SORT** (Simple Online and Realtime Tracking) for object tracking.

These projects demonstrate applications ranging from traffic monitoring to industrial safety compliance and interactive game logic.

## 📋 Table of Contents
- [About](#-about)
- [YOLO Basics & Custom Training](#-yolo-basics--custom-training)
- [Installation](#-installation)
- [Project 1: Car Counter](#-project-1-car-counter)
- [Project 2: People Counter](#-project-2-people-counter)
- [Project 3: PPE Detector](#-project-3-personal-protective-equipment-detector)
- [Project 4: Poker Hand Detector](#-project-4-poker-hand-detector)
- [Directory Structure](#-directory-structure)

---

## 📖 About

This project leverages the **Ultralytics YOLOv8** library combined with **OpenCV**. The core functionality relies on detecting objects frame-by-frame. For the counting projects, the **SORT** algorithm is used to assign unique IDs to objects, allowing the system to track their path and count them as they cross specific coordinates.

### Key Technologies
* **Python 3.x**
* **YOLOv8**: State-of-the-art object detection.
* **OpenCV**: Image processing and video manipulation.
* **SORT**: Algorithm for 2D multiple object tracking.
* **CVZone**: A helper library for easier computer vision visualizations.

---

## 🧠 YOLO Basics & Custom Training

Projects 1 & 2 use pre-trained YOLO weights (`yolov8l.pt`). However, **Project 3 (PPE)** and **Project 4 (Poker)** use custom-trained models (`ppe.pt` and `playingCards.pt`).

### How Custom Training Works:
1.  **Data Collection**: Images are gathered for specific classes (e.g., playing cards, hardhats).
2.  **Annotation**: Images are labeled using tools like **Roboflow** or **LabelImg**.
3.  **Training**: The model is trained on this data to create a custom `.pt` file.
    ```python
    from ultralytics import YOLO
    model = YOLO("yolov8n.pt")
    model.train(data="dataset.yaml", epochs=100)
    ```

---

## ⚙️ Installation

1.  **Clone the repository**:
    ```bash
    git clone [https://github.com/yourusername/your-repo-name.git](https://github.com/yourusername/your-repo-name.git)
    ```

2.  **Install Dependencies**:
    ```bash
    pip install ultralytics opencv-python cvzone filterpy scikit-image lapx
    ```
    *Note: `lapx` is required for the linear assignment in SORT.*

3.  **Download Weights**:
    Ensure you have the required weights inside a `Yolo-Weights` folder or adjust the paths in the code.
    * `yolov8l.pt` (Standard YOLO)
    * `ppe.pt` (Custom trained for PPE)
    * `playingCards.pt` (Custom trained for Cards)

---

## 🚗 Project 1: Car Counter

**File:** `carcounter.py`

A traffic monitoring system that counts vehicles traveling on a highway. It uses a mask to ignore non-road areas and tracks vehicles as they cross a designated line.

* **Classes Detected:** Car, Truck, Bus, Motorbike.
* **Logic:** Uses SORT to track ID. When a vehicle's center crosses the line `[400, 297, 673, 297]`, the count increments.

---

## 👥 Project 2: People Counter

**File:** `Peoplecounter.py`

Designed for escalators or entryways, this project counts people moving **Up** and **Down** separately.

* **Features:**
    * **Bi-Directional Counting:** Separate counters/lines for Up and Down streams.
    * **Visual Interface:** Overlays a custom `graphics.png` to display counts.
    * **Class Filtering:** Strictly detects `Person` (Class ID 0).

---

## 👷 Project 3: Personal Protective Equipment Detector

**File:** `PPE Dectection.py`

**Custom Model:** `ppe.pt`

This project monitors safety compliance on construction sites. It detects workers and safety gear, using color-coded bounding boxes to indicate safety status.

### Safety Logic
The system changes the bounding box color based on the class detected:
* 🔴 **Danger (Red):** `NO-Hardhat`, `NO-Safety Vest`, `NO-Mask`.
* 🟢 **Safe (Green):** `Hardhat`, `Safety Vest`, `Mask`.
* 🔵 **Neutral (Blue):** `Machinery`, `Vehicles`, `Persons` (general).

### Classes Detected
`Excavator`, `Gloves`, `Hardhat`, `Ladder`, `Mask`, `NO-Hardhat`, `NO-Mask`, `NO-Safety Vest`, `Person`, `SUV`, `Safety Cone`, `Safety Vest`, `machinery`, `vehicle`, etc.

---

## 🃏 Project 4: Poker Hand Detector

**Files:** `PokerHandDetector.py`, `PokerHandFunction.py`

**Custom Model:** `playingCards.pt`

A real-time card recognizer that uses game logic to identify the rank of a poker hand.

### How it Works
1.  **Detection:** YOLO detects specific cards (e.g., `10H`, `KD`, `AC`) with high confidence (>0.5).
2.  **Collection:** It aggregates detected cards into a list.
3.  **Hand Logic (`PokerHandFunction.py`):**
    * Once **5 unique cards** are found, the hand is analyzed.
    * It checks for: **Royal Flush**, **Straight Flush**, **Four of a Kind**, **Full House**, **Flush**, **Straight**, **Three of a Kind**, **Two Pair**, **Pair**, and **High Card**.
4.  **Display:** The detected hand rank is displayed on the screen.

---

## 📂 Directory Structure

Ensure your project folder is organized as follows for the code to run without path errors:
