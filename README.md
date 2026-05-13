# GeoAgent-VLM: Tool-Augmented Remote Sensing Reasoning

## Project Overview
This project explores hallucination reduction and multi-hop reasoning improvement in Vision Language Models (VLMs) for remote sensing imagery. 

While the project initially explored the LLaVA architecture, the final pipeline utilizes **Qwen2-VL** to leverage its Naive Dynamic Resolution and superior spatial instruction-following. To eliminate cascading perception errors and rigorously test spatial logic, we implemented an agentic ReAct-style framework combined with **Oracle GeoTools** (derived from GeoJSON ground truth) and **Recurrent Visual Attention Masking (RVAM)**.

## Required Datasets
To run this notebook in Kaggle, you must attach the following two datasets to your environment:
1. **xView Dataset (Images & Annotations):**
   - URL: [https://www.kaggle.com/datasets/hassanmojab/xview-dataset](https://www.kaggle.com/datasets/hassanmojab/xview-dataset)
   - Contains the high-resolution satellite imagery and the `xView_train.geojson` file required for the Oracle tools.
2. **Project Weights & Results Cache:**
   - URL: [https://www.kaggle.com/datasets/mohammadaliabdullah/weights](https://www.kaggle.com/datasets/mohammadaliabdullah/weights)
   - Contains pre-calculated benchmark files, masked image caches, and LoRA weights to speed up execution.

## Hardware Requirements
- **Environment:** Kaggle Notebooks
- **Accelerator:** GPU T4 x2 (or P100). The Qwen2-VL 7B model is loaded using 4-bit NormalFloat (nf4) quantization via `bitsandbytes` to fit within Kaggle's 15GB/16GB VRAM limits.

## How to Run & Navigate the Notebook
The notebook is structured sequentially. We highly recommend running the notebook using **Run All**.

### Phase 1: Setup & Benchmark Generation
- **Dependencies:** Installs `qwen-vl-utils`, `transformers>=4.47.0`, and optimized quantization libraries.
- **Unbiased Benchmark:** Programmatically parses the `xView_train.geojson` file to generate a perfectly balanced (50% Yes / 50% No) 600-question spatial benchmark across 2-Hop, 3-Hop, and 4-Hop complexities. 
- *Path Configuration:* Ensure `GEOJSON_PATH` and `IMAGE_DIR` point to the mounted `/kaggle/input/datasets/hassanmojab/xview-dataset/...` directory.

### Phase 2: Multimodal Infrastructure & Oracle Tools
- Loads **Qwen2-VL-7B-Instruct** into memory.
- Defines the `GeoTools` class (`scene_inventory`, `spatial_query`, `visual_masker`). These tools use perfect mathematical knowledge of the scene to isolate the LLM's *logical reasoning* from *perceptual failures*.

### Phase 3: The Dual-Evaluation Pipeline
- Evaluates the questions in two modes simultaneously:
  1. **Baseline VQA:** Standard zero-shot prompting.
  2. **GeoAgent (ReAct):** The model enters a multi-step loop, executing tools and dynamically modifying the image tensor (via OpenCV Gaussian Blurs in RVAM) to re-direct attention.

### Phase 4: Strict Scoring & Visualization
- Uses word-boundary Regular Expressions (`\b`) to eliminate "chatty" false positives in the model's text generation.
- Automatically generates a Seaborn comparative bar chart showcasing the performance delta between the Baseline and the GeoAgent framework.

## Authors
- Muhammad Sheis Hussain
- Ali Abdullah
- Manal Haider
