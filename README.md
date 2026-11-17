# Threat-Vision
Real-time intruder detection and threat segmentation system using YOLOv8, U-Net, and MobileNetV3 — deployed on GPU with live React dashboard.
ThreatVision AI is an end-to-end real-time surveillance system 
that detects intruders, segments threat regions pixel-by-pixel, 
and instantly clears the threat area in the video feed while 
blurring the background.

Two-stage pipeline:
→ Stage 1: YOLOv8n detects persons and weapons every frame (<10ms)
→ Stage 2: MobileNetV3 violence classifier triggers on positives
→ U-Net ResNet34 segments the threat region and applies video clearing

Features:
- 8.5ms pipeline latency on T4 GPU
- Live WebSocket video streaming
- React dashboard with real-time alert logging
- REST API built with FastAPI
- Docker ready for cloud deployment

Stack: YOLOv8 · U-Net · MobileNetV3 · FastAPI · 
       React · WebSocket · Docker · PyTorch · COCO


## Pipeline

![Threat Vision pipeline](threat-vision-pipeline.png)

## Files

| File | Purpose |
|---|---|
| `fine_tuning.py` | Fine-tunes the U-Net (ResNet34) segmentation model |
| `u_net_video_clearing.py` | Runs the full detection, classification and video-clearing pipeline, and serves it with FastAPI over WebSocket |
| `App.jsx`, `ThreatDashboard.jsx` | React dashboard: live video feed and alert log |
| `threat-vision-pipeline.png` | Pipeline diagram |

## Running it

Both Python scripts were written in **Google Colab** with a T4 GPU, and start with `!pip install` cells. Open them in Colab and run them top to bottom.

`u_net_video_clearing.py` uses ngrok to expose the API, and reads the token from Colab secrets (`NGROK_TOKEN`). Add your token there and never paste it into the code.
