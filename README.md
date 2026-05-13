# GeoAgent: Overcoming Step Degradation in Geospatial VLMs

**GitHub Repository:** [https://github.com/Ali-Abdullah-1921/DL-project](https://github.com/Ali-Abdullah-1921/DL-project)

## Project Overview
This project explores hallucination reduction and multi-hop reasoning improvement in Vision Language Models (VLMs) applied to remote sensing imagery. 

Through an iterative development process, the project evolved from standard VQA baselines to an advanced Agentic AI system. The final "V2" architecture utilizes **Qwen2-VL** (for Naive Dynamic Resolution) paired with an agentic ReAct-style loop, **Oracle GeoTools**, and **Gaussian Recurrent Visual Attention Masking (RVAM)** to physically ground the model's spatial logic and eliminate "step degradation."

## Project Progression & Methodology
The project and this repository are structured around three core development phases:

### Task 3: Baseline
- **Execution:** Evaluated a standard **LLaVA-1.5 (7B)** model on a custom, mathematically balanced 600-question multi-hop benchmark generated from xView GeoJSON data.
- **Findings:** The baseline suffered heavily from linguistic hallucinations. A "Blind Stress Test" (using black images) proved the model was exploiting language priors rather than visual evidence.

### Task 4: First Improvement
- **Execution:** Introduced a **ReAct Agentic Framework** utilizing LLaVA-1.5 alongside specialist vision tools (**YOLOv8-OBB** and **SAM**). We also introduced an early version of RVAM using solid black boxes to mask objects.
- **Findings:** While this grounded the model, it introduced a *Compounding Error Penalty*. If YOLO missed a 5-pixel car due to noise, the agent failed the logic task. Furthermore, solid black masks caused destructive spatial interference by hiding adjacent terrain.

### Task 5: Second Improvement (Final Architecture)
- **Execution:** We transitioned to **Qwen2-VL-7B-Instruct** for superior instruction following. To isolate true reasoning from predictive detector failures, we replaced YOLO with **Oracle GeoTools** (derived directly from ground-truth GeoJSON). We also upgraded RVAM to use **Gaussian Blurs**, scrambling discriminative features without destroying spatial context.
- **Results:** This architecture achieved massive performance gains, improving strict 4-hop spatial reasoning accuracy from **53.0% (Baseline) to 84.5% (GeoAgent)**.

## Integrity Testing Suite (Validation)
To confirm the pipeline is working correctly and the results are scientifically valid, the notebook runs several automated audits:
- **Blind Stress Test:** Feeds the agent a completely black image to ensure it correctly fails.
- **Scoring Rigidity (Poisoned Data Test):** Inverts the ground truth to guarantee the regex-based grader isn't handing out false positives.
- **Reasoning Bypass Audit:** Scans the agent's internal thought process to flag "Lucky Guesses" (correct answers achieved without tool calls).

## Required Datasets & Setup
To run the included notebook (`deep-learning-project-baseline.ipynb`) in Kaggle, attach the following datasets:
1. **xView Dataset:** [https://www.kaggle.com/datasets/hassanmojab/xview-dataset](https://www.kaggle.com/datasets/hassanmojab/xview-dataset)
2. **Project Weights & Results Cache:** [https://www.kaggle.com/datasets/mohammadaliabdullah/weights](https://www.kaggle.com/datasets/mohammadaliabdullah/weights)

## Authors
- Mohammad Ali Abdullah (26100241)
- Muhammad Sheis Hussain (26100220)
- Manal Haider (27100024)
