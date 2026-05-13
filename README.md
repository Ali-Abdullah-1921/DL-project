# GeoAgent-VLM: Tool-Augmented Remote Sensing Reasoning

## Project Overview
This project explores hallucination reduction and multi-hop reasoning improvement in Vision Language Models (VLMs) for remote sensing imagery. 

Through an iterative development process, the project evolved from standard VQA baselines to an advanced Agentic AI system. The final "V2" architecture utilizes **Qwen2-VL** (for Naive Dynamic Resolution) paired with an agentic ReAct-style loop, **Oracle GeoTools**, and **Recurrent Visual Attention Masking (RVAM)** using Gaussian blurs to physically ground the model's spatial logic.

## Breakthrough Results
The V2 Architecture effectively eliminates the "step degradation" bottleneck typically seen in spatial reasoning. By mathematically isolating the VLM's logic and using RVAM to tether attention, the GeoAgent achieved massive performance gains over the baseline:
* **2-Hop Accuracy:** 89.5% (Baseline: 57.0%)
* **3-Hop Accuracy:** 83.0% (Baseline: 59.5%)
* **4-Hop Accuracy:** 84.5% (Baseline: 53.0%)

## Methodology & Notebook Progression
The included Jupyter Notebook (`deep-learning-project-baseline.ipynb`) contains the complete research progression:

### 1. Phase 1: Baseline
- **Architecture:** Vanilla LLaVA-1.5 (7B).
- **Execution:** Evaluated on a custom, mathematically balanced 600-question multi-hop benchmark generated from xView GeoJSON data.

### 2. Phase 2: Agentic Framework (V1)
- **Architecture:** LLaVA-1.5 + LoRA Fine-tuning (GeoChat format).
- **Tools:** Integrated YOLOv8-OBB for detection and Meta's SAM for segmentation.
- **Masking:** Utilized solid black boxes to mask objects and redirect attention.
- *Limitation Discovered:* Cascading perceptual errors from YOLO and destructive spatial interference from solid black masks hindered true multi-hop reasoning.

### 3. V2: The Bulletproof Dual-Evaluation Pipeline (Final)
- **Architecture:** Transitioned to **Qwen2-VL-7B-Instruct** for superior instruction following and dynamic resolution scaling.
- **Tools:** Replaced YOLO with **Oracle GeoTools** (derived directly from ground-truth GeoJSON) to isolate the VLM's logical reasoning from perceptual detector failures.
- **Masking (RVAM):** Replaced solid black boxes with **Gaussian Blurs**, which scramble discriminative object features while preserving adjacent terrain and spatial context.

## Required Datasets & Setup
To run this notebook in Kaggle, attach the following datasets to your environment:
1. **xView Dataset (Images & Annotations):** [https://www.kaggle.com/datasets/hassanmojab/xview-dataset](https://www.kaggle.com/datasets/hassanmojab/xview-dataset)
2. **Project Weights & Results Cache:** [https://www.kaggle.com/datasets/mohammadaliabdullah/weights](https://www.kaggle.com/datasets/mohammadaliabdullah/weights)

## Authors
- Muhammad Sheis Hussain
- Ali Abdullah
- Manal Haider
