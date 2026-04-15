🚗 YOLOv5 Object Detection in CARLA (Day → Night Generalization)

## 📌 Project Summary

In this project, we worked on an object detection system using **YOLOv5** in the CARLA simulator.

The main idea was to **train the model in well-lit (daytime) conditions and then test how it performs in low-light / night-time scenarios**.

👉 This helps us understand how well the model handles **real-world changes in lighting**, which is important for autonomous driving.

---

## 🏆 What we achieved

* Trained the model on **daytime simulation data**
* Tested it in **night-time conditions**
* Results:

  * **mAP@0.5:** 98.5% (training conditions)
  * **mAP@0.5–0.95:** 85.7% (night-time testing)

💡 We noticed that the model still performs well overall, but:

* **Pedestrians are detected very accurately**
* **Vehicle detection drops slightly**, mainly due to fewer samples and low visibility

---

## 🧠 Problem we explored

Most models work well in the same conditions they were trained on, but struggle when the environment changes.

So we wanted to check:

> What happens if a model trained in bright conditions is used at night?

---

## 🏗️ How we did it

### 1. Data Collection

* Used **CARLA simulator**
* Captured RGB images and segmentation data
* Generated our own dataset

### 2. Preprocessing

* Converted annotations from **XML (VOC) → YOLO format**
* Applied simple augmentations:

  * Reduced brightness
  * Added blur to simulate night conditions

### 3. Model Training

* Model: **YOLOv5s**
* Image size: 640 × 640
* Epochs: 25
* Split: 80% training / 20% validation

### 4. Deployment

* Ran the model inside CARLA
* Set environment to **night-time**
* Performed real-time object detection using ego vehicle camera

---

## ⚙️ Setup Instructions

### 1. Clone the repo

```bash
git clone https://github.com/Nithya-Kanakam/yolov5-carla-nighttime-object-detection.git
cd yolov5-carla-nighttime-object-detection
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Clone YOLOv5

```bash
git clone https://github.com/ultralytics/yolov5
cd yolov5
pip install -r requirements.txt
```

---

## 📂 Dataset

The dataset was generated using CARLA.

👉 Due to size, it is not included in this repo
👉 You can download it here: **[ADD YOUR LINK]**

Structure:

```bash
dataset/
├── images/
│   ├── train/
│   └── val/
├── labels/
│   ├── train/
│   └── val/
```

---

## 🏋️ Training

```bash
python train.py --img 640 --batch 16 --epochs 25 --data ../data.yaml --weights yolov5s.pt --name yolov5_carla
```

---

## 🎮 Running the Model (Deployment)

```bash
python ../src/deploy.py
```

This will:

* Start CARLA simulation
* Load the trained model (`best.pt`)
* Show real-time detections in night conditions

---

## 📊 Results

| Metric       | Value |
| ------------ | ----- |
| Precision    | 99.3% |
| Recall       | 95.4% |
| mAP@0.5      | 98.5% |
| mAP@0.5–0.95 | 85.7% |

### 🔍 Observations

* Pedestrians → very accurate
* Trees → consistent detection
* Vehicles → lower performance (less data + low visibility)

---

## 📷 Sample Output

(Add some screenshots here — this really helps show your work)

---

## 🔦 Key Takeaway

Training in one condition and testing in another (day → night) clearly shows that:

* Models are sensitive to lighting changes
* Dataset diversity is important
* Real-world deployment is more challenging than training

---

## 📁 Project Structure

```bash
├── src/
│   ├── data.py
│   ├── xml_to_txt.py
│   ├── deploy.py
│
├── dataset_sample/
├── results/
├── docs/
│   ├── PPT.pdf
│   ├── description.docx
│
├── data.yaml
├── requirements.txt
└── README.md
```

---

## 🚀 Future Work

* Add more vehicle data to balance classes
* Include different weather conditions (rain, fog)
* Try improving low-light performance using better augmentation or domain adaptation

---

## 👥 Team

* Nithya Kanakam
* Keerthana Kothakapu Adamulla

---

## ⭐ Final Note

This project helped us understand how object detection models behave when conditions change, which is very important for real-world autonomous systems.
