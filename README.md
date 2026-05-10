# GeoAgent-VLM: Tool-Augmented Remote Sensing Reasoning

## Project Overview
This project explores hallucination reduction and multi-hop reasoning improvement in Vision Language Models (VLMs) for remote sensing imagery.

The work builds on the LLaVA architecture and introduces an agentic ReAct-style framework combined with external vision tools for grounded spatial reasoning.

## Methodology
The project consists of three major phases:

### 1. Baseline
- Evaluated LLaVA on remote sensing benchmark questions
- Tested multi-hop reasoning performance on aerial imagery

### 2. Improvement 1
- Applied instruction-aligned prompting and lightweight adaptation techniques
- Improved robustness for remote sensing queries

### 3. Improvement 2
- Implemented a tool-augmented ReAct framework
- Integrated YOLO-based object detection for grounded reasoning
- Added masking and regex-based evaluation pipelines

## Technologies Used
- Python
- PyTorch
- HuggingFace Transformers
- LLaVA
- YOLOv8
- Kaggle Notebooks

## Repository Contents
- Final project notebook

## Authors
- Muhammad Sheis Hussain
- Ali Abdullah
- Manal Haider
