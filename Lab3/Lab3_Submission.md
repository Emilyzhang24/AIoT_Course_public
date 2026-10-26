# Lab 3 Submission Report
## On-Device AI Deployment on XIAO ESP32-S3

**ECE 4930/6930 – Artificial Intelligence of Things**

---

# Team Information

| Item | Response |
|---|---|
| Team Number | |
| Date | |
| Member 1 | |
| Member 2 | |
| Member 3 | |

**Both tasks are required:**

- [ ] Task A — Pretrained SenseCraft Gesture Recognition
- [ ] Task B — Custom AI Model with Edge Impulse

Submit **one report per team**.

> [!NOTE]
> Focus on documenting your experiments and observations. Brief answers are sufficient.
> Model accuracy does not need to be perfect. If a technical issue prevents successful deployment, document the error and what you tried.

---

# Part 1 — Hardware and Setup

Record the basic hardware information.

| Item | Response |
|---|---|
| Hardware platform | Seeed Studio XIAO ESP32S3 Sense |
| Sensor(s) used | |
| Arduino ESP32 board-package version (Task B) | |
| PSRAM setting (Task B) | |

---

# Part 2 — Task A: Pretrained Gesture Recognition

Deploy a pretrained gesture-recognition model using SenseCraft AI.

## Part 2A — Model Information

| Item | Response |
|---|---|
| Pretrained model name | |
| Model source/link | |
| Gesture labels | |

## Part 2B — Gesture Recognition Results

Perform **five gesture trials**. Test at least two different gestures when possible.

| Trial | Intended Gesture | Model Prediction | Correct? |
|---|---|---|---|
| 1 | | | |
| 2 | | | |
| 3 | | | |
| 4 | | | |
| 5 | | | |

**Correct predictions:** _____ / 5

> [!NOTE]
> This is a small functional test, not a formal measurement of model accuracy.

## Part 2C — Deployment Evidence

Provide a screenshot or short video showing gesture recognition running on the **physical XIAO board**.

**Screenshot or video link:**

## Part 2D — Observation

### A-Q1. What is one observation about the gesture model's behavior?

For example, did it recognize all gestures correctly? Did lighting, distance, or hand position affect the results?

**Answer (1–2 sentences):**

---

# Part 3 — Task B: Custom AI Application

Select a small AI application, train a lightweight model in Edge Impulse, and deploy it to the physical XIAO.

The human-versus-dog classification in the demonstration video is an example of the workflow. Your team may choose a different application.

## Part 3A — Application and Model Information

| Item | Response |
|---|---|
| AI application / task | |
| Sensor input (camera or microphone) | |
| Class labels or model outputs | |
| Edge Impulse project/model name or link | |
| Model type and input size, if applicable | |
| Number of training samples | |
| Number of testing samples | |
| Tutorial or example adapted, if any | |

## Part 3B — Model Testing in Edge Impulse

Record the model-testing result and one representative prediction.

| Item | Result |
|---|---|
| Test accuracy or task-specific metric | |
| Example test input | |
| Expected result | |
| Model prediction | |

**Model Testing screenshot or example link (if available):**

## Part 3C — Deployment Estimates

Record the following Edge Impulse estimates, if available.

| Metric | Estimated Value |
|---|---|
| Device used for estimation | |
| Inference latency (ms) | |
| Flash/ROM (KB) | |
| RAM (KB) | |

> [!IMPORTANT]
> These are deployment estimates, not necessarily measurements on the XIAO.
> If a metric is unavailable, enter `N/A`.

---

# Part 4 — On-Device Deployment and Testing

## Part 4A — Deployment Evidence

Provide evidence showing that **both models ran on the physical XIAO board**.

| Task | Screenshot or Video Link |
|---|---|
| Task A — Pretrained gesture recognition | |
| Task B — Custom model inference | |

For Task B, evidence may include the Arduino Serial Monitor showing live predictions or a short video of the working board.

A separate Arduino upload screenshot is **not required** if the on-device inference evidence clearly demonstrates successful deployment.

## Part 4B — Task B Live Inference Tests

Perform **three live tests** using your custom model.

Try different input conditions when practical.

| Trial | Input / Test Condition | Expected Result | Model Prediction |
|---|---|---|---|
| 1 | | | |
| 2 | | | |
| 3 | | | |

For applications other than image classification, record the relevant model output.

## Part 4C — On-Device Inference Timing (If Available)

If the running program reports inference timing, record three readings.

| Trial | Latency (ms) |
|---|---:|
| 1 | |
| 2 | |
| 3 | |

**Median on-device latency:** __________ ms / `N/A`

**Timing field used:** __________ / `N/A`

If inference timing is not displayed, enter `N/A`. No additional timing code is required.

## Part 4D — Observation

### B-Q1. How did your custom model perform during live testing? Describe one successful result, limitation, or deployment issue.

**Answer (2–3 sentences):**

---

# Part 5 — AIoT Reflection

### R-Q1. What did you learn from deploying both a pretrained model and a custom model on the XIAO?

Briefly discuss:

- One difference between Task A and Task B.
- One limitation or tradeoff of running AI on the XIAO compared with the Jetson Nano.

**Answer (3–5 sentences):**

---

# Submission Checklist

Before submitting, confirm that:

- [ ] Team and hardware information is complete.
- [ ] Task A model information and five gesture trials are included.
- [ ] Task A on-device inference evidence is included.
- [ ] Task B application, dataset, and model-testing results are included.
- [ ] Task B on-device inference evidence and three live tests are included.
- [ ] Available performance estimates and on-device timing are recorded, with `N/A` where necessary.
- [ ] The three short written questions are answered.
- [ ] **One report is submitted per team.**

---

**Lab Instructions:** [Lab 3 Instruction](Lab3_Instruction.md)
