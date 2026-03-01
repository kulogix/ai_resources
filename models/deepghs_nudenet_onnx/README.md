---
pipeline_tag: object-detection
tags:
- not-for-all-audiences
- onnx
- yolov8
- nsfw-detection
license: apache-2.0
library_name: onnxruntime
---

# NudeNet ONNX Models

## Summary

This repository provides **optimized ONNX models** for the **NudeNet object detection system**, originally developed by notAI-tech. The models are designed for **efficient nudity detection** in images using a YOLOv8-based architecture with specialized training for NSFW content recognition. These ONNX-format models enable **cross-platform compatibility** and accelerated inference across various hardware backends.

The implementation includes two key components: a **YOLOv8 detection model** (`320n.onnx`) for generating initial bounding box proposals and a **non-maximum suppression module** (`nms-yolov8.onnx`) for post-processing and filtering duplicate detections. The system can identify 18 different anatomical regions and clothing states, including both exposed and covered body parts with high precision.

Performance is optimized through **model quantization** and ONNX Runtime integration, providing significant speed improvements over the original implementation while maintaining detection accuracy. The models operate on 320x320 input resolution and support configurable detection thresholds for balancing precision and recall according to specific application requirements.

## Usage

### Installation

```bash
pip install onnxruntime>=1.18.0
# For GPU acceleration (optional):
# pip install onnxruntime-gpu>=1.18.0
pip install dghs-imgutils
```

### Basic Detection

```python
from imgutils.detect.nudenet import detect_with_nudenet
from PIL import Image

# Load and process image
image = Image.open('your_image.jpg')
detections = detect_with_nudenet(
    image, 
    topk=100,
    iou_threshold=0.45,
    score_threshold=0.25
)

# Process results
for bbox, label, confidence in detections:
    x1, y1, x2, y2 = bbox
    print(f"Detected {label} with confidence {confidence:.3f} at [{x1:.1f}, {y1:.1f}, {x2:.1f}, {y2:.1f}]")
```

## Original Content

ONNX models of [notAI-tech/NudeNet](https://github.com/notAI-tech/NudeNet).

### Label Definitions

Here is a detailed list of labels from the NudeNet detection model and their respective meanings:

| Label | Description |
|-------|-------------|
| FEMALE_GENITALIA_COVERED | Detects covered female genitalia in the image. |
| FACE_FEMALE | Detects the face of a female in the image. |
| BUTTOCKS_EXPOSED | Detects exposed buttocks in the image. |
| FEMALE_BREAST_EXPOSED | Detects exposed female breasts in the image. |
| FEMALE_GENITALIA_EXPOSED | Detects exposed female genitalia in the image. |
| MALE_BREAST_EXPOSED | Detects exposed male breasts in the image. |
| ANUS_EXPOSED | Detects exposed anus in the image. |
| FEET_EXPOSED | Detects exposed feet in the image. |
| BELLY_COVERED | Detects a covered belly in the image. |
| FEET_COVERED | Detects covered feet in the image. |
| ARMPITS_COVERED | Detects covered armpits in the image. |
| ARMPITS_EXPOSED | Detects exposed armpits in the image. |
| FACE_MALE | Detects the face of a male in the image. |
| BELLY_EXPOSED | Detects an exposed belly in the image. |
| MALE_GENITALIA_EXPOSED | Detects exposed male genitalia in the image. |
| ANUS_COVERED | Detects a covered anus in the image. |
| FEMALE_BREAST_COVERED | Detects covered female breasts in the image. |
| BUTTOCKS_COVERED | Detects covered buttocks in the image. |

## Citation

```bibtex
@misc{nudenet_onnx,
  title        = {{NudeNet ONNX Models}},
  author       = {deepghs and notAI-tech},
  howpublished = {\url{https://huggingface.co/deepghs/nudenet_onnx}},
  year         = {2023},
  note         = {Optimized ONNX models for the NudeNet object detection system, providing efficient nudity detection with YOLOv8 architecture},
  abstract     = {This repository provides optimized ONNX models for the NudeNet object detection system, originally developed by notAI-tech. The models are designed for efficient nudity detection in images using a YOLOv8-based architecture with specialized training for NSFW content recognition. These ONNX-format models enable cross-platform compatibility and accelerated inference across various hardware backends. The implementation includes two key components: a YOLOv8 detection model for generating initial bounding box proposals and a non-maximum suppression module for post-processing and filtering duplicate detections.},
  keywords     = {object-detection, onnx, yolov8, nsfw-detection}
}
```
