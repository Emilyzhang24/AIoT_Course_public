# Lab 2 Submission Report
## Efficient Edge AI — From Model Complexity to Real Deployment

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

---

# Part 1 — Common Benchmark: ResNet-18 vs. ResNet-50

## Part 1A — Prediction

### P1-Q1. Which model did your team expect to have lower network latency?

```text


```

### P1-Q2. Did you expect the latency ratio to be approximately equal to the GMAC ratio?

- [ ] Yes
- [ ] No

Explain briefly:

```text



```

---

## Part 1B — ResNet-18 Measurements

| Trial | Network CUDA Latency (ms) |
|---|---:|
| 1 | |
| 2 | |
| 3 | |

**Median Network Latency:**

```text
____________ ms
```

**Predicted Class:**

```text


```

**Confidence:**

```text


```

---

## Part 1C — ResNet-50 Measurements

| Trial | Network CUDA Latency (ms) |
|---|---:|
| 1 | |
| 2 | |
| 3 | |

**Median Network Latency:**

```text
____________ ms
```

**Predicted Class:**

```text


```

**Confidence:**

```text


```

---

## Part 1D — Model Comparison

Use the theoretical values and equations from:

[Reference Metrics and Formulas](Reference_Metrics.md)

| Metric | ResNet-18 | ResNet-50 |
|---|---:|---:|
| Parameters | | |
| Approx. GMACs | | |
| Model File Size | | |
| Median Network Latency (ms) | | |
| Network FPS | | |

---

### Theoretical GMAC Ratio

```text
Calculation:


Result:
```

---

### Measured Latency Ratio

```text
Calculation:


Result:
```

---

## Part 1E — Analysis


### P1-Q3. Was the measured latency increase proportional to the increase in theoretical GMACs?

- [ ] Approximately yes
- [ ] No

Explain using your measurements:

```text




```

### P1-Q4. If the theoretical and measured ratios were different, identify at least two possible reasons.

**Reason 1**

```text


```

**Reason 2**

```text


```

### P1-Q5. Based on your results, is theoretical model complexity alone sufficient for selecting an edge-AI model?

Explain using your measurements.

```text




```

---

# Part 2 — Efficient-AI Exploration

## Track Selection

Which track(s) did your team complete?

- [ ] **Track Q — Reduced Precision**
- [ ] **Track R — Real-Time Edge-System Efficiency**
- [ ] **Track P — Pruned-Model Deployment Case Study**

Complete only the section(s) corresponding to the track(s) your team attempted.

---

# Track Q — Reduced Precision

## Track Q1 — Prediction

### Q-Q1. Did you expect FP16 to provide higher throughput than FP32?

- [ ] Yes
- [ ] No

### Q-Q2. Did you expect approximately 2× higher throughput?

- [ ] Yes
- [ ] No

Explain your prediction:

```text



```

---

## Track Q2 — FP32 Measurements

| Reading | Throughput (img/sec) |
|---|---:|
| 1 | |
| 2 | |
| 3 | |

**Average FP32 Throughput:**

```text
____________ img/sec
```

---

## Track Q3 — FP16 Measurements

| Reading | Throughput (img/sec) |
|---|---:|
| 1 | |
| 2 | |
| 3 | |

**Average FP16 Throughput:**

```text
____________ img/sec
```

---

## Track Q4 — Throughput Speedup

Use the definition from:

[Reference Metrics and Formulas](Reference_Metrics.md)

```text
Calculation:


Result: ____________ ×
```

---

## Track Q5 — Analysis

### Q-Q3. Did FP16 improve throughput, and was the measured improvement close to 2×?

Support your answer using your average throughput values and calculated speedup.

```text



```

### Q-Q4. Why does reducing numerical precision not guarantee a proportional runtime improvement?

```text




```

### Q-Q5. How does this FP32/FP16 experiment relate to INT8 quantization discussed in class?

```text




```

---

# Track R — Real-Time Edge-System Efficiency

Complete this section only if your team attempted **Track R**.

## Track R1 — Hypothesis

### R-Q1. Before running live inference, how did your team expect ResNet-18 and ResNet-50 to compare?

Consider Network FPS and Jetson resource usage.

```text




```

---

## Track R2 — Measurements

| Metric | ResNet-18 | ResNet-50 |
|---|---:|---:|
| Network FPS | | |
| RAM Usage | | |
| GPU Utilization | | |
| CPU Utilization | | |
| GPU Temperature | | |
| Power, if reported | | |

---

## Track R3 — Analysis

### R-Q2. Which model placed greater demand on the Jetson?

Support your answer with at least one measured value.

```text




```

### R-Q3. Was the performance difference observed in Part 1 also visible during continuous inference?

Explain using the single-image latency and live Network FPS measurements.

```text




```

### R-Q4. Which hardware or performance measurement was most useful for comparing the two models?

```text




```

### R-Q5. Why can continuous inference reveal deployment behavior that may not be obvious from a single-image benchmark?

```text




```

---

# Track P — Pruned-Model Deployment Case Study

Complete this section only if your team attempted **Track P**.

## Track P1 — Models Tested

**Original Model:**

```text


```

**Pruned / Optimized Model:**

```text


```

---

## Track P2 — Measurements

| Metric | Original Model | Pruned / Optimized Model |
|---|---:|---:|
| Network CUDA Latency (ms) | | |
| Model File Size, if measured | | |
| Detection Result | | |
| Confidence / Other Observation | | |

---

## Track P3 — Latency Speedup

Use the definition from:

[Reference Metrics and Formulas](Reference_Metrics.md)

```text
Calculation:


Result: ____________ ×
```

---

## Track P4 — Analysis

### P-Q1. Did the pruned/optimized model run faster?

```text




```

### P-Q2. Did you observe any difference in detection behavior?

```text




```

### P-Q3. Does your result support the statement:

> "Fewer weights automatically produce proportional latency reduction."

- [ ] Yes
- [ ] No

Explain:

```text




```

### P-Q4. Why might structured pruning be easier for TensorRT/GPU hardware to exploit than unstructured sparsity?

```text




```

### P-Q5. Why should this PeopleNet comparison not be interpreted as a perfectly controlled pruning-only experiment?

```text




```

---

# Efficient-AI Connection

Even if your team did not experimentally test every technique, connect your results to the efficient-AI concepts discussed in class.

| Technique | Main Change | Expected Edge Benefit | What Still Needs Hardware Measurement? |
|---|---|---|---|
| Reduced Precision / Quantization | | | |
| Pruning | | | |
| Knowledge Distillation | | | |

---

### E-Q1. Suppose a distilled student model has fewer parameters and fewer GMACs than its teacher. What deployment benefits would you hope to observe, and which of those benefits would still need to be measured on the Jetson??

```text




```

---

# Edge-Deployment Recommendation

Assume you are developing an always-on AIoT application using this Jetson Nano.

The system should provide:

- useful AI predictions;
- reasonable inference speed;
- manageable resource demand;
- stable continuous operation.

---

## Recommended Model or Optimization Strategy

```text



```

---

## Experimental Evidence

Provide at least three pieces of evidence from your Lab 2 measurements.

### Evidence 1

```text


```

### Evidence 2

```text


```

### Evidence 3

```text


```

---

### D-Q1. Why did your team select this model or optimization strategy?

```text





```

### D-Q2. What tradeoff did your team accept in making this decision?

Examples may include:

- model capability vs. latency;
- model size vs. speed;
- throughput vs. resource demand;
- numerical precision vs. performance.

```text




```

---

# Final Reflection

### D-Q3. In 3–5 sentences, explain why efficient-AI models should still be evaluated on the actual target hardware.

Consider that efficient-AI methods are often described using:

- parameter count,
- FLOPs,
- numerical precision,
- sparsity.

```text






```

---

# Submission Checklist

Before submitting, confirm:

- [ ] Team information is complete.
- [ ] Part 1 prediction questions are complete.
- [ ] Three ResNet-18 latency measurements are recorded.
- [ ] Three ResNet-50 latency measurements are recorded.
- [ ] Median latency is reported for both models.
- [ ] Model-size results are recorded.
- [ ] GMAC ratio and latency ratio are calculated.
- [ ] Network FPS is reported for both models.
- [ ] At least one Part 2 exploration track is documented.
- [ ] All questions for each completed Part 2 track are answered.
- [ ] Efficient-AI connection questions are complete.
- [ ] The deployment recommendation is supported by experimental evidence.
- [ ] Final reflection is complete.
- [ ] One report is submitted per team.
