# Jetson-Inference Reference

## What Is Jetson-Inference?

Jetson-Inference is a software framework for running pretrained deep-learning
models on NVIDIA Jetson devices.

It provides examples for several common computer-vision tasks, including:

- Image classification
- Object detection
- Semantic segmentation
- Pose estimation

In this course, Jetson-Inference is already installed on the shared Jetson systems. 
You do **not** need to reinstall it unless specifically instructed.
Find more here: https://github.com/dusty-nv/jetson-inference/tree/master#inference

---

## Where Is Jetson-Inference?

The shared repository is located at:

```bash
~/jetson-inference
```

The compiled inference programs are located at:

```bash
~/jetson-inference/build/aarch64/bin
```

To enter this directory:

```bash
cd ~/jetson-inference/build/aarch64/bin
```

You can inspect the available programs with:

```bash
ls imagenet* detectnet* segnet* posenet*
```

---

# 1. Image Classification

## What Does Classification Do?

Image classification assigns an entire image to one or more categories.

For example:

```text
Input Image
    ↓
Neural Network
    ↓
"orange"
```

The model answers:

> What is the main object or category in this image?

---

## Example

Navigate to the inference directory:

```bash
cd ~/jetson-inference/build/aarch64/bin
```

Run:

```bash
./imagenet images/orange_0.jpg images/test/output_0.jpg --model=resnet18
```

This command uses:

- **Input:** `images/orange_0.jpg`
- **Model:** ResNet-18
- **Output:** `images/test/output_0.jpg`

Open the result:

```bash
xdg-open images/test/output_0.jpg
```

---

# 2. Object Detection

## What Does Object Detection Do?

Object detection identifies both:

1. what objects are present, and
2. where they are located.

For example:

```text
Input Image
      ↓
Object Detector
      ↓
Person → Bounding Box
Car    → Bounding Box
```

Unlike classification, object detection can identify multiple objects in the
same image.

---

## Example

```bash
cd ~/jetson-inference/build/aarch64/bin
```

Run:

```bash
./detectnet.py --network=ssd-mobilenet-v2 images/peds_0.jpg images/test/output.jpg
```

This example uses:

- **Input:** `images/peds_0.jpg`
- **Model:** SSD-Mobilenet-v2
- **Output:** `images/test/output.jpg`

Open the result:

```bash
xdg-open images/test/output.jpg
```

---

# 3. Semantic Segmentation

## What Does Segmentation Do?

Semantic segmentation assigns a class label to each pixel in an image.

For example:

```text
Input Image
       ↓
Segmentation Network
       ↓
Road pixels     → Road
Car pixels      → Vehicle
Building pixels → Building
```

This produces a more detailed understanding of the scene than classification
or object detection.

---

## Example

```bash
cd ~/jetson-inference/build/aarch64/bin
```

Run:

```bash
./segnet.py --network=fcn-resnet18-cityscapes images/city_0.jpg images/test/output.jpg
```

This example uses:

- **Input:** `images/city_0.jpg`
- **Model:** FCN-ResNet18 trained for Cityscapes
- **Output:** `images/test/output.jpg`

Open the result:

```bash
xdg-open images/test/output.jpg
```

---

# 4. Pose Estimation

## What Does Pose Estimation Do?

Pose estimation detects important human body keypoints, such as:

- shoulders,
- elbows,
- wrists,
- hips,
- knees,
- ankles.

A simplified example is:

```text
Image of Person
      ↓
Pose Network
      ↓
Body Keypoints
      ↓
Skeleton Representation
```

---

## Example

```bash
cd ~/jetson-inference/build/aarch64/bin
```

Run:

```bash
./posenet "images/humans_*.jpg" images/test/pose_humans_%i.jpg
```

The command processes multiple human images and saves the resulting annotated
images.

---

# Comparison of the Four Tasks

| Task | Main Question | Typical Output |
|---|---|---|
| Classification | What is in the image? | Class label and confidence |
| Object Detection | What objects are present and where? | Labels + bounding boxes |
| Semantic Segmentation | What class does each pixel belong to? | Pixel-level class map |
| Pose Estimation | Where are the body joints? | Keypoints / skeleton |

---

# Relationship to AIoT

In an AIoT application, the camera acts as a sensor and Jetson-Inference
provides the AI processing.

A typical pipeline is:

```text
Physical Environment
        ↓
      Camera
        ↓
      Jetson
        ↓
Jetson-Inference
        ↓
AI Model
        ↓
Prediction
        ↓
Application / Decision
```

Different applications may require different inference tasks.

For example:

- Smart camera → object detection
- Scene understanding → segmentation
- Human activity monitoring → pose estimation
- Simple visual recognition → classification

---

# Important Course Note

The Jetson-Inference installation is shared among student teams.

Do not:

- reinstall it,
- delete files from it,
- update it,
- or modify shared models

unless specifically instructed.

Save your team's experimental outputs in your assigned workspace:

```text
~/AIoT_Lab/teamX/outputs/
```

where `teamX` is your assigned team number.
