# Zero-Shot-Bearing-Fault-Detection-by-Blind-Domain-Transition

# Project Description
Continuous long-term monitoring of motor health is crucial for the early detection of abnormalities such as bearing faults (up to 51% of motor failures are attributed to bearing faults). Despite numerous methodologies proposed for bearing fault detection, most of them require normal (healthy) and abnormal (faulty) data for training. Even with the recent deep learning (DL) methodologies trained on the labeled data from the same machine, the classification accuracy significantly deteriorates when one or few conditions are altered, e.g., a different speed or load, or for different fault types/severities with sensors placed in different locations. Furthermore, their performance suffers significantly or may entirely fail when they are tested on another machine with entirely different healthy and faulty signal patterns. To address this need, in this pilot study, we propose a zero-shot bearing fault detection method that can detect any fault on a new (target) machine regardless of the working conditions, sensor parameters, or fault characteristics. To accomplish this objective, a 1D Operational Generative Adversarial Network (Op-GAN) first characterizes the transition between normal and fault vibration signals of (a) source machine(s) under various conditions, sensor parameters, and fault types. Then for a target machine, the potential faulty signals can be generated, and over its actual healthy and synthesized faulty signals, a  compact, and lightweight 1D Self-ONN fault detector can then be trained to detect the real faulty condition in real time whenever it occurs. To validate the proposed approach, a new benchmark dataset is created using two different motors working under different conditions and sensor locations. Experimental results demonstrate that this novel approach can accurately detect any bearing fault achieving an average recall rate of around 89% and 95% on two target machines regardless of its type, severity, and location. 
[Paper Link](https://arxiv.org/abs/2212.06154)


## Qatar University Dual-Machine Bearing Fault Benchmark Dataset: QU-DMBF

![image](https://user-images.githubusercontent.com/98646583/207285515-23333c67-e1fe-41f3-a339-d39a3cfaeb68.png)

The benchmark dataset used in this study was generated by the researchers at Qatar University from two electric machines. Figure 3 shows the installation of two machines (A and B) along with the sensor locations.  For Machine-A, the setup includes a 3-phase AC motor (brand: VEMAT, Model: 3VTB-90LA(2P), Vicena-Italy), whose input frequency was controlled by a variable frequency drive. The motor used in this experiment supplied 2.2 kW (3 Hp) at a maximum speed of 2840 rpm. The vibration signals were acquired by using 5 high sensitivity, ceramic shear ICP accelerometers (from PCB Piezotronics, Model No. 352C33, 100 mV/g, NY-USA), which were fixed on the same mounting base that supported the load cell (from Omegadyne Inc, Model No. LCM204-50KN, Manchester-UK), and 4 other different location on machine and motor. The readings were controlled by two four-channel NI-9234 sound and vibration input modules at a sampling frequency of 4.096 kHz. It has a ~180 kg weight and the setup has 100x100x40 cm dimensions. Machine-A has the following variations on the working conditions:

-	19 different bearing configurations: 1 healthy, 18 fault cases: 9 with a defect on the outer ring, and 9 with a defect on the inner ring. The defect sizes are varying from 0.35mm to 2.35mm.
-	5 different accelerometer localization: 3 different positions and 2 different directions (radial and axial)
-	2 different load (force) levels: 0.12 kN and 0.20 kN. 
-	3 different speeds: 480, 680, and 1010 RPM. 


Machine B, on the other hand, was originally a Machinery Fault Simulator from SpectraQuest Inc, USA. The setup includes a DC motor of 0.37 kW (0.5 HP), 90 VDC, 5 A, with a maximum rotational speed of 2500 RPM. The original shaft of the machine was removed and replaced by a new and bigger one to accommodate the same bearings used on Machine-A. For the sake of resistance and stability, other supporting mechanical components were also redesigned. The machine has an approximate weight of 50kg and overall dimensions of 100x63x53 cm.   Machine-B has the following variations on the working conditions:

-	19 different bearing configurations: 1 healthy, 9 with a defect on the outer ring, and 9 with a defect on the inner ring. The defect sizes are varying from 0.35mm to 2.35mm.
-	6 different accelerometer positions.
-	A fixed load (force) of 0.15 kN. 
-	5 different speeds: 240, 360, 480, 700, and 1020 RPM
- Full QU-DMBF dataset with user manual can be downloaded from the given [link](https://drive.google.com/drive/folders/1glUH3mLPUowrwi-B0yrIWHWm_ZpNfnBN?usp=share_link)
## Run

#### Train
- Training/Validation/Test dataset for two motors can be downloaded from the given [link](https://drive.google.com/drive/folders/1glUH3mLPUowrwi-B0yrIWHWm_ZpNfnBN?usp=share_link). Download train, validation and test data to the "tmats/", "vmats/", and "temats/" folders folders respectively. 
- Start training (Stage-1)
```http
  python Op_GAN_train.py
```
- Faulty Data Synthesis (Stage-2). You can download Pre-trained Network [weights](https://drive.google.com/drive/folders/1LNi5dd2TXROzAQxQBDG3oSSp30JEJ9XJ?usp=sharing)
```http
  python Op_GAN_test.py
```
- Save outputs to the "goutputs/" folder. 

- Prepeare Training Data for classifier. Save outputs to the "classifier/mats/" folder.  
```http
  data_prepeare.m
```
- Start training the classifier (Stage-3) 
```http
  python Classifier_train.py
```
- Fault Detection (Stage-4) 
```http
  python Classifier_test.py
```

## Prerequisites
- Pyton 3
- Pytorch
- [FastONN](https://github.com/junaidmalik09/fastonn) 


  
## Results

![image](https://user-images.githubusercontent.com/98646583/207303899-b35256d6-24a3-4f41-9ad4-3c2b2520e0e7.png)

## Citation
If you find this project useful, we would be grateful if you cite this paper：

```http
S. Kiranyaz, O. C. Devecioglu, A. Alhams, S. Sassi, T. Ince, O. Abdeljaber, O. Avci, T. Hamid, R. Mazhar, A. Khandakar, A. Tahir, T. Rahman, and M. Gabbouj, “Zero-Shot Motor Health Monitoring by Blind Domain Transition ”
```


