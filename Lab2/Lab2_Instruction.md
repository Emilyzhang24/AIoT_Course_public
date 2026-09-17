# Lab 2: Efficient Edge AI — From Model Complexity to Real Deployment

**ECE 4930/6930 – Artificial Intelligence of Things**

> [!NOTE]
> **Total time:** One 75-minute class session  
> **Platform:** Seeed Studio reComputer with NVIDIA Jetson Nano  
> **Camera:** Sony IMX219 CSI camera  
> **Software:** Jetson-Inference / TensorRT

---

## Overview

In Lab 1, you verified the Jetson platform, camera, software environment, and basic AI inference.

In Lab 2, the focus shifts from:

> **Can the Jetson run AI?**

to:

> **How efficiently can AI models run on the Jetson, and how should we choose a model for edge deployment?**

You will compare:

- **theoretical model complexity**, such as parameters and MACs/FLOPs; and
- **measured edge performance**, such as latency, network FPS, throughput, and Jetson resource usage.

The main experimental workflow is:

```text
AI Model
   ↓
Theoretical Complexity
   ↓
TensorRT Inference
   ↓
Measured Performance
   ↓
Jetson Hardware Behavior
   ↓
Edge Deployment Decision
```

This lab connects directly to efficient-AI methods discussed in class:

- efficient model architectures,
- reduced numerical precision,
- pruning,
- knowledge distillation.

For definitions of latency, network FPS, throughput, model storage, and hardware measurements, refer to:

[Reference Metrics and Formulas](Reference_Metrics.md)

---

# Learning Objectives

After completing this laboratory, you will be able to:

- distinguish theoretical model complexity from measured inference performance;
- compare AI models using parameters, MACs, latency, and network FPS;
- use TensorRT timing information to evaluate inference performance;
- explain why fewer FLOPs do not necessarily produce proportional speedup;
- investigate an efficient-AI strategy on real edge hardware;
- evaluate tradeoffs among model capability, latency, and hardware resources;
- make an evidence-based edge-deployment recommendation.

---

# Before You Begin

The Jetson-Inference environment and required ResNet models were prepared previously.

Use the team workspace created in Lab 1:

```text
~/aiot_Course/teams/teamX/
```

Do not reinstall Jetson-Inference or upgrade:

- JetPack,
- CUDA,
- cuDNN,
- TensorRT,
- or the operating system.

Unless an exploration track specifically allows an additional model, use models already available on the Jetson.

---

# Laboratory Structure

This laboratory contains two experimental parts.

| Part | Activity | Suggested Time |
|---|---|---:|
| **Part 1** | Common benchmark: theoretical complexity vs. measured performance | 25–30 min |
| **Part 2** | Efficient-AI exploration | 35–40 min |

All teams must complete **Part 1**.

Then complete **at least one** exploration track from Part 2.

If your team completes the first exploration track with more than approximately 15 minutes remaining, begin a second track.

> [!IMPORTANT]
> Completing more tracks is not the primary objective.
>
> The quality of your measurements, experimental comparison, and interpretation is more important than the number of experiments completed.

Record measurements during the laboratory.

Complete the final interpretation and deployment recommendation in the **Lab 2 Submission Report**.

---

# Part 1 — Common Benchmark: ResNet-18 vs. ResNet-50

The first experiment asks:

> **Does a model with more theoretical computation require proportionally more inference time on the Jetson?**

Use the same input image for both networks.

The theoretical parameter and GMAC values are provided in:

[Reference Metrics and Formulas](Reference_Metrics.md)

Before running the experiment, predict:

1. Which model will have lower network latency?
2. Will the latency ratio be approximately equal to the GMAC ratio?

Record your prediction before continuing.

---

## Step 1 — Benchmark ResNet-18

Navigate to:

```bash
cd ~/aiot_Course/jetson-inference/build/aarch64/bin
```

Run:

```bash
./imagenet images/orange_0.jpg \
~/aiot_Course/teams/teamX/outputs/resnet18_lab2.jpg \
--network=resnet-18 \
--profile
```

Replace `teamX` with your team number.

Locate the TensorRT timing report. Record the:

```text
Network CUDA time
```

as the **network latency**.

Repeat the experiment three times. Use the Lab 2 Submission Report to record the three measurements, predicted class, confidence, and median network latency.


> [!NOTE]
> The first execution may involve additional initialization. Repeated measurements help reduce the influence of timing variability.

---

## Step 2 — Benchmark ResNet-50

Run:

```bash
./imagenet images/orange_0.jpg \
~/aiot_Course/teams/teamX/outputs/resnet50_lab2.jpg \
--network=resnet-50 \
--profile
```

Again, run the experiment three times.

Use the Lab 2 Submission Report to record the three `Network` CUDA latency measurements, predicted class, confidence, and median network latency.

---

## Step 3 — Compare Model Storage

Locate the ResNet model files:

```bash
find ~/aiot_Course/jetson-inference/data/networks \
-maxdepth 2 -type f | grep -i resnet
```

For each relevant model file, use:

```bash
du -h <MODEL_FILE>
```

Record the model-file size.

> [!NOTE]
> Model-file size is different from runtime RAM usage.
>
> Runtime memory also includes activations, TensorRT buffers, CUDA memory, and application data.

---

## Step 4 — Calculate the Performance Metrics

Using the definitions and formulas in:

[Reference Metrics and Formulas](Reference_Metrics.md)

calculate:

- theoretical GMAC ratio;
- measured latency ratio;
- network FPS for ResNet-18;
- network FPS for ResNet-50.

Use the **median Network CUDA latency** from the three trials for all latency-based calculations.

Record the results for use in the Lab 2 Submission Report.

---

# Part 2 — Efficient-AI Exploration

Complete **at least one** track.

If time remains, begin a second track.

| Track | Question | Additional Model Required? |
|---|---|---|
| **Track Q** | Does reduced numerical precision improve Jetson throughput? | Possibly GoogLeNet |
| **Track R** | What happens during sustained real-time edge inference? | No |
| **Track P** | Does an available pruned/optimized model provide a deployment benefit? | Yes |

---

# Track Q — Reduced Precision on the Jetson

## Question

> **Does reducing numerical precision from FP32 to FP16 improve inference throughput on this Jetson?**

This track connects to the lecture discussion of quantization and reduced-precision inference.

FP16 is not integer quantization, but it provides a practical way to study the broader idea:

```text
Lower Numerical Precision
        ↓
Potentially Lower Memory / Compute Cost
        ↓
Potential Hardware Speedup
```

The word **potentially** is important.

---

## Step Q1 — Check `trt-bench`

Navigate to:

```bash
cd ~/aiot_Course/jetson-inference/build/aarch64/bin
```

Check whether the benchmark exists:

```bash
ls trt-bench
```

If the file is not found, select another Part 2 track.

This version of `trt-bench` uses a GoogLeNet classification model internally.

Check whether GoogLeNet is available:

```bash
ls ~/aiot_Course/jetson-inference/data/networks/Googlenet
```

If it exists, continue to Step Q3.

If not, either try the optional download below or select another track.

Do not spend more than approximately **5 minutes** troubleshooting a model download.

---

## Step Q2 — Optional GoogLeNet Download

To try the Jetson-Inference model downloader:

```bash
cd ~/aiot_Course/jetson-inference/tools
./download-models.sh
```

Select:

```text
GoogLeNet
```

If the download fails or takes too long, stop and select Track R instead.

Then return to:

```bash
cd ~/aiot_Course/jetson-inference/build/aarch64/bin
```

---

## Step Q3 — Make a Prediction

Before benchmarking, predict:

1. Will FP16 provide higher throughput than FP32?
2. Will FP16 be exactly 2× faster because it uses half as many bits?

Record your prediction.

---

## Step Q4 — Benchmark FP32

Run:

```bash
./trt-bench --image=images/orange_0.jpg --GPU=FP32
```

Allow the benchmark to run until the reported values become reasonably stable.

Record three consecutive:

```text
img/sec
```

measurements.

Use the Lab 2 Submission Report to record three consecutive stable throughput measurements.

Stop with:

```text
Ctrl + C
```

---

## Step Q5 — Benchmark FP16

Run:

```bash
./trt-bench --image=images/orange_0.jpg --GPU=FP16
```

Again allow the benchmark to stabilize.

Use the Lab 2 Submission Report to record three consecutive stable throughput measurements.

Stop with:

```text
Ctrl + C
```

---

## Step Q6 — Compare FP32 and FP16

Using the **Throughput Speedup** definition in:

[Reference Metrics and Formulas](Reference_Metrics.md)

calculate the average throughput for each precision and the resulting throughput speedup.

Complete the Track Q analysis in the Lab 2 Submission Report.

> [!NOTE]
> INT8 is not required in this laboratory.
>
> INT8 deployment commonly requires a calibrated or otherwise compatible quantized model, making it less suitable as a required activity in this 75-minute lab.

---

# Track R — Real-Time Edge-System Efficiency

**Recommended / guaranteed track — no additional downloads required**

## Question

> **How do two models with different computational complexity behave during continuous inference on the Jetson?**

This experiment extends the single-image benchmark from Part 1 to a continuous camera workload.

---

## Step R1 — Form a Hypothesis

Before running the experiment, predict how ResNet-18 and ResNet-50 will compare during continuous inference.

Consider:

- Network FPS;
- RAM usage;
- GPU utilization;
- CPU utilization;
- GPU temperature.

Record your hypothesis for use in the Lab 2 Submission Report.

---

## Step R2 — Run ResNet-18 with the CSI Camera

Navigate to:

```bash
cd ~/aiot_Course/jetson-inference/build/aarch64/bin
```

Run:

```bash
./imagenet.py csi://0 --network=resnet-18
```

Allow the application to run for approximately 20–30 seconds.

While live inference is running, observe the displayed:

```text
Network XX FPS
```

---

## Step R3 — Monitor ResNet-18 Hardware Usage

Open a second terminal and run:

```bash
tegrastats
```

Observe the system while inference is running.

Use the Lab 2 Submission Report to capture the requested Network FPS and system measurements.

Stop the inference application with:

```text
Ctrl + C
```

---

## Step R4 — Run ResNet-50

Repeat the same procedure using:

```bash
./imagenet.py csi://0 --network=resnet-50
```

Again allow the application to run for approximately 20–30 seconds.

Record:

- representative Network FPS;
- one representative `tegrastats` sample.

Use the same observation procedure that you used for ResNet-18.

---

## Step R5 — Save Your Measurements

Record the measurements for both models for use in the Lab 2 Submission Report.

Compare the live measurements with the single-image results obtained in Part 1.

---

# Track P — Pruned-Model Deployment Case Study

> [!NOTE]
> This is an exploratory deployment comparison rather than a perfectly controlled pruning-only experiment.
>
> The available PeopleNet and pruned PeopleNet packages may differ in more than pruning configuration.
>
> Therefore, investigate whether the available optimized model provides a deployment benefit, but do not attribute every measured difference exclusively to pruning.

## Question

> **Does the available pruned/optimized model provide a measurable deployment benefit on the Jetson?**

Jetson-Inference supports PeopleNet variants including:

```text
peoplenet
peoplenet-pruned
```

> [!IMPORTANT]
> Attempt Track P only if both PeopleNet models are already available on the Jetson.
>
> If either model is unavailable, select Track R instead. Model downloading is not required or optional for completing Lab 2.

---

## Step P1 — Check Available Models

Navigate to:

```bash
cd ~/aiot_Course/jetson-inference/build/aarch64/bin
```

Check the supported detection networks:

```bash
./detectnet.py --help
```

Then check which network files are already installed:

```bash
ls ~/aiot_Course/jetson-inference/data/networks
```

---

## Step P2 — Obtain a Model if Needed

If you choose this track and one of the required models is missing:

```bash
cd ~/aiot_Course/jetson-inference/tools
./download-models.sh
```

Look for the PeopleNet models supported by the installed Jetson-Inference version.

> [!IMPORTANT]
> Use the model downloader associated with this Jetson-Inference installation.
>
> Do not manually install a newer arbitrary PeopleNet package because the teaching Jetsons use an older JetPack/TensorRT environment.

If downloading fails or takes more than approximately **5 minutes**, switch to Track R.

---

## Step P3 — Run the Original Model

Return to:

```bash
cd ~/aiot_Course/jetson-inference/build/aarch64/bin
```

Run:

```bash
./detectnet.py \
--network=peoplenet \
images/peds_0.jpg \
~/aiot_Course/teams/teamX/outputs/peoplenet_lab2.jpg \
--profile
```

Record:

- Network CUDA latency;
- detected objects;
- confidence, if reported.

---

## Step P4 — Run the Pruned Model

Run:

```bash
./detectnet.py \
--network=peoplenet-pruned \
images/peds_0.jpg \
~/aiot_Course/teams/teamX/outputs/peoplenet_pruned_lab2.jpg \
--profile
```

Record the same measurements.

---

## Step P5 — Compare the Two Models

Using the **Latency Speedup** definition from:

[Reference Metrics and Formulas](Reference_Metrics.md)

compare:

- Network CUDA latency;
- detection behavior;
- model storage, if easily available.

If time permits, run both models using the CSI camera and compare their live Network FPS.

Record your observations for use in the Lab 2 Submission Report.

> [!NOTE]
> This comparison is an exploratory deployment case study.
>
> The available PeopleNet and pruned PeopleNet packages may differ in more than pruning configuration, so measured differences should not be attributed exclusively to pruning.

---

# Knowledge Distillation Connection

Knowledge distillation is not implemented directly in this 75-minute laboratory because producing a distilled student requires a teacher model, training data, and an additional training process.

Conceptually:

```text
Large Teacher
      ↓
Knowledge Transfer
      ↓
Smaller Student
      ↓
Target Edge Hardware
```

The experiments in this lab illustrate the same deployment principle:

> A theoretically smaller or more efficient model should still be evaluated on the target hardware before its practical benefit is assumed.

Use your Jetson measurements to discuss this connection in the Lab 2 Submission Report.

---

# After the Experiments

Complete the:

[Lab 2 Submission Report](Lab2_Submission.md)

using the measurements collected during the laboratory.

Submit one report per team.
