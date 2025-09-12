# Image Classification GUI (ResNet-50 + PyQt5)

## Overview
This project implements a **desktop application** for image classification using a **pretrained ResNet-50 model** from PyTorch’s `torchvision` library.  
The application provides a **Graphical User Interface (GUI)** built with **PyQt5**, enabling users to classify images either from their **webcam** or from a **local file**.  

Predictions are made on the **ImageNet-1K dataset**, and both the **predicted class name** and the **associated probability score** are displayed on the image in real time.

---

## Technical Details

### Model
- **Architecture**: [ResNet-50](https://arxiv.org/abs/1512.03385)
- **Pretrained Weights**: `ResNet50_Weights.IMAGENET1K_V1`
- **Dataset**: ImageNet-1K (1,000 classes)
- **Framework**: PyTorch (`torch` and `torchvision`)

The model outputs a tensor of shape `(1, 1000)`, corresponding to the probability distribution over all ImageNet classes. The top-1 prediction is extracted using `torch.topk`.

---

### Preprocessing Pipeline
All images undergo the following preprocessing before inference:
1. **Resize** to 256 pixels on the shorter side  
2. **CenterCrop** to 224 × 224  
3. **Convert to Tensor**  
4. **Normalize** using ImageNet statistics:
   - Mean = `[0.485, 0.456, 0.406]`
   - Std = `[0.229, 0.224, 0.225]`

These transformations are defined using `torchvision.transforms`.

---

### GUI Design
The interface is implemented with **PyQt5**.  

Main components:
- **Main Window (`App`)**
  - Live webcam feed using `cv2.VideoCapture`
  - Buttons for:
    - *Capture Image from Webcam*
    - *Load Image from Computer*
  - Live preview of the webcam stream
- **Capture Window (`CaptureWindow`)**
  - Displays the captured or loaded image
  - Runs classification
  - Draws predicted class and probability directly on the image using OpenCV + QPainter

---

### External Dependencies
- **PyTorch**: Model inference
- **Torchvision**: Pretrained ResNet-50 and transforms
- **OpenCV**: Webcam capture, image handling
- **PyQt5**: GUI framework
- **Pillow (PIL)**: Image loading and conversion
- **Requests + JSON**: Fetch ImageNet class labels


