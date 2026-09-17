# Reference Metrics and Formulas

This laboratory uses four types of information.

| Metric | Source | Meaning |
|---|---|---|
| Parameters / GMACs | Instructor-provided reference | Theoretical model complexity |
| Model file size | `du -h` | Storage required by the model |
| Network latency / FPS | Jetson-Inference profiler | Measured neural-network execution performance |
| RAM / GPU / temperature | `tegrastats` | Measured Jetson resource usage |

---

## 1. Network Latency

For this lab:

> **Network latency is the CUDA execution time reported for the `Network` row in the Jetson-Inference timing report.**

Run the model with:

```bash
--profile
```

Look for output similar to:

```text
[TRT] Timing Report
...
Network       CPU ... ms   CUDA ... ms
...
```

Record the:

```text
Network CUDA time
```

in milliseconds.

Do not use:

- model-loading time;
- total command execution time;
- preprocessing time;
- program startup time.

unless explicitly requested.

---

## 2. Network FPS

Network FPS estimates how many neural-network inferences could be completed per second based on network latency.

Use:

```text
Network FPS = 1000 / Network latency_ms
```

Example:

```text
Network latency = 25 ms

Network FPS = 1000 / 25 = 40 FPS
```

Jetson-Inference uses the same relationship internally when reporting network FPS.

> [!NOTE]
> This is **network-only FPS**. It does not necessarily equal camera FPS or end-to-end application FPS because image capture, preprocessing, postprocessing, rendering, and communication may add additional delay.

---

## 3. Benchmark Throughput

Some experiments use `trt-bench`.

`trt-bench` repeatedly executes inference and directly reports:

```text
img/sec
```

For example:

```text
24.5 img/sec
```

In this lab, call this:

> **Benchmark throughput**

Do not calculate it from the single-image profiler result. Record the value directly from `trt-bench`.

When comparing two configurations:

```text
Throughput Speedup =
Optimized img/sec / Baseline img/sec
```

---

## 4. Model Storage

Use:

```bash
du -h <MODEL_FILE>
```

to measure model storage.

Model storage is different from runtime RAM usage.

---

## 5. Jetson Resource Usage

Use:

```bash
tegrastats
```

to observe:

- RAM usage;
- GPU utilization;
- CPU utilization;
- GPU temperature;
- power, if reported.

Record representative values while inference is actively running.

---

# Theoretical vs. Measured Quantities

The following values are provided as theoretical references:

| Model | Parameters | Approx. Compute |
|---|---:|---:|
| ResNet-18 | ~11.7 M | ~1.8 GMACs |
| ResNet-50 | ~25.6 M | ~4.1 GMACs |

Students do not need to calculate these values from the Jetson.

Use them to compare theoretical model complexity with measured Jetson performance.

For example:

```text
Theoretical comparison:
ResNet-50 GMACs / ResNet-18 GMACs

Measured comparison:
ResNet-50 network latency / ResNet-18 network latency
```

The central question is:

> Does the measured latency increase in proportion to the theoretical increase in model computation?
