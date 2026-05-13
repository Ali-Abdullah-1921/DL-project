# GeoAgent-VLM: Tool-Augmented Remote Sensing Reasoning

## Project Overview
This project explores hallucination reduction and multi-hop reasoning improvement in Vision Language Models (VLMs) for remote sensing imagery. 

Through an iterative development process, the project evolved to the final "V2" architecture: an advanced Agentic AI system utilizing **Qwen2-VL**, **Oracle GeoTools**, and **Recurrent Visual Attention Masking (RVAM)**. Crucially, this repository features a comprehensive **Integrity Testing Suite** designed to mathematically prove that the model's spatial reasoning is genuine and not the result of linguistic hallucination or metric gaming.

## Breakthrough Results
The V2 Architecture effectively eliminates the "step degradation" bottleneck. By mathematically isolating the VLM's logic and using RVAM to tether attention, the GeoAgent achieved massive performance gains over the baseline:
* **2-Hop Accuracy:** 89.5% (Baseline: 57.0%)
* **3-Hop Accuracy:** 83.0% (Baseline: 59.5%)
* **4-Hop Accuracy:** 84.5% (Baseline: 53.0%)

## Methodology & Notebook Progression
The included Jupyter Notebook (`deep-learning-project-baseline.ipynb`) contains the complete research progression:

### 1. The V2 GeoAgent Pipeline
- **Architecture:** **Qwen2-VL-7B-Instruct** for superior instruction following and dynamic resolution scaling.
- **Tools:** **Oracle GeoTools** (derived directly from ground-truth GeoJSON) to isolate the VLM's logical reasoning from perceptual detector failures.
- **Masking (RVAM):** **Gaussian Blurs** scramble discriminative object features while preserving adjacent terrain, physically forcing the model's attention to shift.

### 2. The Integrity & Validation Testing Suite (Core Focus)
To confirm the pipeline is working correctly and the results are scientifically valid, the notebook runs several automated audits:
- **Blind Stress Test (Hallucination Baseline):** Feeds the agent a completely black image to ensure it correctly fails (proving it doesn't just memorize questions).
- **Scoring Rigidity (Poisoned Data Test):** Inverts the ground truth to guarantee the regex-based grader isn't "leaking" or handing out false positives.
- **Reasoning Bypass Audit:** Scans the agent's internal thought process to flag "Lucky Guesses"—instances where the model got the right answer but bypassed tool usage.
- **Agent Psychoanalysis:** Automatically isolates and prints the specific step-by-step reasoning traces of failed questions for qualitative debugging.

## Required Datasets & Setup
To run this notebook in Kaggle, attach the following datasets to your environment:
1. **xView Dataset (Images & Annotations):** [https://www.kaggle.com/datasets/hassanmojab/xview-dataset](https://www.kaggle.com/datasets/hassanmojab/xview-dataset)
2. **Project Weights & Results Cache:** [https://www.kaggle.com/datasets/mohammadaliabdullah/weights](https://www.kaggle.com/datasets/mohammadaliabdullah/weights)

## Authors
- Muhammad Sheis Hussain
- Ali Abdullah
- Manal Haider
