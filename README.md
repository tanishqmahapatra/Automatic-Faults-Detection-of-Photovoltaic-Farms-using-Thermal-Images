<h1 align="center"><ins>Automatic Faults Detection of Photovoltaic Farms using Thermal Images</ins></h1>
<br>

<h4 align="center">
<b><ins>EXPLORATORY PROJECT</ins></b>
</h4>

## Table of contents

<ol>
  <li><a href="#abstract">Abstract</a></li>
  <li><a href="#introduction">Introduction</a></li>
  <li>
    <a href="#model-and-algorithm">Model and Algorithm</a>
    <ul>
      <li><a href="#yolov5">YOLOv5</a></li>
      <li><a href="#dataset-preparations">Data Preparations</a></li>
      <li>
        <a href="#predictions-made">Predictions Made</a>
        <ul>
          <li><a href="#pv-array-detection">PV Array Detection</a></li>
          <li><a href="#single-pv-module-detection">Single PV Module Detection</a></li>
          <li><a href="#pv-module-with-fault">PV Module with Fault</a></li>
        </ul>
      </li>
      <li><a href="#setup-requirements">Model Setup Requirements</a></li>
      <li><a href="#initialisation">Initialisation</a></li>
    </ul>
  </li>
  <li><a href="#types-of-faults">Types of Faults</a></li>
  <li><a href="#results-and-prediction-scores">Results and Prediction Scores</a></li>
</ol>

# Abstract

- Because of increasing demand for renewable energy, proper management of photovoltaic hubs is important. However, fault detection in them remains a challenge. The main temperature-consequenced faults can be detected using thermal analysis of PV modules. In this paper, we used **YOLOv5 (You Look Only Once version 5)** for detections, which is a novel state-of-the-art convolutional neural network (CNN) that detects objects in real-time with great accuracy. This approach uses a single neural network to process the entire image, then divides it into parts and predicts bounding boxes and probabilities for each component. Using YOLOv5, we detected:
  - **Photovoltaic array module**
  - **Single PV module**
  - **Faulted PV module (based on temperature variation)**

- This model will be used in a UAV quadcopter for detection of faults on the Vellore Institute of Technology Chennai campus. It will be uploaded using Ardu-Mission Planner in the Pixhawk, with a Jetson Nano used as the companion computer.

# Introduction

Today, renewable energy sources are revolutionizing the energy generation sector and represent the only alternative to limit fossil fuel usage. Due to increasing demand, the renewable energy sector must be managed in a way that fulfills the ever-growing requirements and demands. The most common and widely used renewable source is photovoltaic (PV) power plants, which are a key system for producing clean energy. Monitoring the state of health of PV systems and ensuring their proper operation is essential for maintaining maximum efficiency. However, due to the large area of solar farms, current techniques are time-consuming, cause energy generation to stop, and often require laboratory instrumentation, making them not cost-effective for frequent inspections. Moreover, PV plants are often located in inaccessible places, making interventions dangerous.

Automated fault and error detection in solar plants is a highly active area of research. In this paper, we have used the YOLOv5 deep learning network to detect solar panels and faults in thermal images of a solar farm. Photovoltaic modules consist of PV cell circuits sealed in an environmentally protective laminate and are the fundamental building blocks of PV systems. Photovoltaic panels include one or more PV modules assembled as a pre-wired, field-installable unit. A photovoltaic array is the complete power-generating unit, consisting of any number of PV modules and panels. Irradiance and temperature are key factors determining the efficiency of PV modules and can be used as parameters for fault detection in PV arrays.

# Model and Algorithm

### **<ins>YOLOv5</ins>**

YOLO, an acronym for 'You Only Look Once,' is an object detection algorithm that divides images into a grid system. Each cell in the grid is responsible for detecting objects within itself. YOLO is one of the most famous object detection algorithms due to its speed and accuracy.

YOLOv5 is preferred above other versions of YOLO because it is about 88% smaller than YOLOv4 (27 MB vs 244 MB), about 180% faster (140 FPS vs 50 FPS), and is roughly as accurate as YOLOv4 on the same task (0.895 mAP vs 0.892 mAP).

### **<ins>Dataset Preparations</ins>**

The dataset used for this project is a **Photovoltaic thermal image dataset**. The thermographic inspection of a ground-based PV system was carried out on a PV plant with a power of approximately 66 MW in Tombourke, South Africa. The thermographic acquisitions were made over seven working days, from 21 to 27 January 2019. The dataset contains three folders, each containing 1009 images of size **512 x 640 pixels**.

For YOLO to work, bounding boxes are required around the object of interest. We created bounding boxes around the faulty cells and strings using masked images provided. For PV array and single cell detection, bounding boxes were made using app.roboflow.com.

### **<ins>Predictions Made</ins>**

Predictions are reasonably accurate, with no false positives detected.

#### **<ins>PV Array Detection</ins>**

PV array detection has yielded the best results among all three detections during validation and testing. The model has almost perfect weights for PV array detection.

#### **<ins>Single PV Module Detection</ins>**

Single PV cell detection model predictions are also fairly accurate. However, the model sometimes considers 2-3 PV modules as a single separated cell and occasionally misses some boundary cells.

#### **<ins>PV Module with Fault</ins>**

Faulty cell detections are accurate for both single defected cells and contiguous sequences of defective cells.

### **<ins>Model Setup Requirements</ins>**

| Requirements | Link(s) |
|--------------|---------|
| [python3](https://www.python.org/downloads/) | [torch-python](https://pytorch.org/) |
| [Bounding box maker](https://app.roboflow.com/) | [Exploratory Repository](https://github.com/Tanishq-Mahapatra/Automatic-Faults-Detection-of-Photovoltaic-Farms-using-Thermal-Images) |

### **<ins>Initialisation</ins>**

1. Git clone the repository.
2. Open the command prompt or terminal with your specific Python environment and type `pip install requirements.txt`.
3. Place the test thermal image in the false-color folder.
4. Run the `detect_teen.py` file with your Python interpreter.
5. Results will be displayed on the screen and saved in the runs folder.

# Types of Faults

- **Physical Faults:**
  - **Soiling Fault:** Detection of faults due to dirt, which can be identified by local temperature variation.
  - **Diode Fault:** Detection of defects in specific parts of the diode screen of the panel.

- **Electrical Faults:**
  - These faults mostly affect the entire PV array or string. Future work will involve detecting electrical faults using inverter parameters and machine learning classifiers.

# Autonomous Drone Navigation

- Scripts have been simulated in ROS (Noetic and Ubuntu 20.0) and Gazebo (version 10) to make the UAV quadcopter fully autonomous and capable of capturing images on its own. 
- However, complete testing in simulation was not possible due to the lack of a thermal camera plugin in Gazebo.

# Conclusion

In this project, YOLOv5, a novel deep learning model, was used for detecting faults in large-scale PV farms and plants. The model is planned to be deployed on a Jetson Nano as a companion computer in a UAV copter. The design of the copter is nearly complete in simulation.

# References

- [Fault detection, classification, and protection in solar photovoltaic arrays](https://repository.library.northeastern.edu/files/neu:rx917d168/fulltext.pdf)
- [HDJSE_6960328 1..11 (hindawi.com)](https://downloads.hindawi.com/journals/js/2020/6960328.pdf)
- [Classification and Detection of Faults in Grid-Connected Photovoltaic Systems](https://www.ijser.org/researchpaper/Classification-and-Detection-of-Faults-in-Grid-Connected-Photovoltaic-Systems.pdf)
