# Lab 1: Edge AI Platform and Baseline Inference

## Submission Sheet

> **Submission Format**
>
> Complete this sheet as a team.
>
> You may:
>
> - keep this page open on a laptop during the laboratory,
> - print it and record observations by hand,
> - or copy it into Microsoft Word / Google Docs.
>
> For final submission, insert the requested screenshots/results and submit **one PDF per team** through Canvas.

---

## Team Information

**Team Number:** ______________________________________
**Date:** _____________________________________________

### Team Members

1. _________________________________________________
2. _________________________________________________
3. _________________________________________________

---

# Part 1 – Hardware Overview

### Q1. Role of the Jetson

Briefly describe the role of the Jetson in an AIoT system.

**Answer:**



---

### Q2. CSI Camera

Why might an embedded AI system use a CSI camera instead of a conventional USB webcam?

**Answer:**



---

# Part 2 – System Verification

Complete the following table.

| Item | Your Observation |
|---|---|
| Ubuntu version | <br><br> |
| Jetson / L4T release | <br><br> |
| JetPack version | <br><br> |
| CPU architecture/model | <br><br> |
| Number of CPU cores | <br><br> |
| Installed / available RAM | <br><br> |

---

# Part 3 – Resource Monitoring

Run:

```bash
tegrastats
```

Insert one representative screenshot or copy a representative portion of the output.

### `tegrastats` Result

**Insert screenshot/output here:**



---

Complete the following table.

| Measurement | Your Observation |
|---|---|
| RAM usage | <br><br> |
| CPU utilization | <br><br> |
| CPU frequency | <br><br> |
| GPU activity/utilization, if reported | <br><br> |
| GPU temperature | <br><br> |
| Power, if reported | <br><br> |


### Q3. Resource Monitoring

Why is monitoring CPU, GPU, memory, power, and temperature important when deploying AI on an edge device?

**Answer:**



---

# Part 4 – Camera Verification

Run:

```bash
v4l2-ctl --list-devices
```

Copy the relevant output below.

```text
PASTE YOUR OUTPUT HERE
```

Complete the table.

| Item | Your Observation |
|---|---|
| Camera sensor | <br><br> |
| Linux video device | <br><br> |
| Camera/interface type | <br><br> |

### Q4. Linux Video Device

What does `/dev/video0` represent?

**Answer:**



---

### Q5. Camera Data Path

Explain the following data path in your own words:

```text
Physical Scene
      ↓
Camera
      ↓
CSI
      ↓
Jetson Video Input
      ↓
/dev/video0
      ↓
AI Application
```

**Answer:**



---

# Part 5 – Team Workspace

### Team Directory

Record your team's workspace location.

```text
________________________________________________________
```

For example:

```text
~/AIoT_Lab/team1/
```

Confirm that your team has separate locations for:

- [ ] inputs
- [ ] outputs
- [ ] notes


---

# Part 6 – Edge AI Software Environment

Navigate to the shared Jetson-Inference repository and run:

```bash
git rev-parse HEAD
```

### Jetson-Inference Commit ID

```text
________________________________________________________
```

### Q6. Reproducibility

Why is recording the Git commit ID useful for a laboratory experiment or research project?

**Answer:**



---

# Part 7 – Baseline AI Inference

For the required baseline experiment, use **image classification with ResNet-18**.

| Item | Your Experiment |
|---|---|
| AI task | Image classification |
| Model/network used | <br><br> |
| Input image | <br><br> |
| Predicted class | <br><br> |
| Output image | <br><br> |

If your team completed an additional optional inference task, record it below.

**Optional task:** ______________________________________

---

## Baseline Inference Result

Insert one representative output image or screenshot.

**Figure 1. Baseline AI inference result**

**Insert image/screenshot here:**



---

### Q7. Input and Output

What information did the AI model receive as input, and what did it produce as output?

**Answer:**



---

### Q8. Location of Inference

Where was the AI inference performed?

- [ ] Jetson edge device
- [ ] Remote cloud server
- [ ] Laptop/workstation
- [ ] Other: ___________________________

Explain briefly.

**Answer:**



---


# Part 8 – Live Camera Inference (If Time Permits)

Was live CSI-camera inference completed?

- [ ] Yes
- [ ] No

If yes, complete the following.

| Item | Observation |
|---|---|
| AI task | <br><br> |
| Model/network | <br><br> |
| One example of good performance | <br><br><br> |
| One unexpected or incorrect result | <br><br><br> |

If available, insert one screenshot.

**Figure 2. Live camera inference result**

**Insert screenshot here:**



If this part was not completed, briefly state why.

**Comment:**



---

# Part 9 – AIoT Reflection

### Q9. Edge versus Cloud AI

Give at least **two advantages** of performing AI inference at the edge instead of sending all raw sensor data to the cloud.

1. 


2. 


---

### Q10. GPU Acceleration

Why is GPU acceleration useful for deep-learning inference?

**Answer:**



---

### Q11. Sensing and Communication

Why might a complete AIoT system require both sensing and wireless communication?

**Answer:**



---

### Q12. End-to-End AIoT Pipeline

Using what you observed in this laboratory, explain the following pipeline:

```text
Physical Environment
        ↓
      Sensor
        ↓
   Edge Computing
        ↓
    AI Inference
        ↓
      Decision
        ↓
Communication / Application
```

**Answer:**



---

# Optional Challenge

If your team completed an optional exploration, describe one additional finding.

### Topic Investigated

_____________________________________________

### Finding



---

# Submission Checklist

Before submitting your report, verify that it includes:

- [ ] Team information
- [ ] Part 1 – Hardware Overview
- [ ] Part 2 – System Verification
- [ ] Part 3 – Resource Monitoring
- [ ] Part 4 – Camera Verification
- [ ] Part 5 – Team Workspace
- [ ] Part 6 – Edge AI Software Environment
- [ ] Part 7 – Baseline AI Inference
- [ ] Part 8 – Live Camera Inference or explanation if not completed
- [ ] Part 9 – AIoT Reflection
- [ ] All required screenshots/results
- [ ] Answers to Questions 1–13

---
