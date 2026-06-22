# Vehicle Number Plate Detection

A system to license plate of the vehicles

## 🚀 Getting Started

### 1. Prerequisites
Ensure you have the following installed on your system:
* **Git**
* **Python 3.8+**
* **PIP** (Python package manager)

### 2. Clone the Repository
Clone the official YOLOv9 repository (or your fork) and navigate into the project directory:

```bash
# Clone the repository
git clone https://github.com/WongKinYiu/yolov9.git

# Navigate into the project folder
cd yolov9
```

Now you are in the directory of the cloned github repo.

#### Environment Setup
It is highly recommended to isolate your dependencies using a virtual environment (venv) to avoid version conflicts with other Python projects on your system.

### 3. Create a Virtual Environment
Run the following command to create a virtual environment named .venv:

#### On Linux/macOS or Windows
```
python -m venv .venv
```

### 4. Activate the Virtual Environment
Activate the environment based on your operating system:

Linux / macOS:
```
source .venv/bin/activate
```

Windows Powershell:
```
python .venv/Scripts/activate
```
Once activated, your terminal prompt will show (.venv) at the beginning.

### 5. Dependency Installation
Install Requirements
With the virtual environment active, upgrade pip and install the required packages (including PyTorch, torchvision, and other dependencies specified by YOLOv9):

```
# Upgrade pip to the latest version
python -m pip install --upgrade pip

# Install dependencies
pip install -r requirements.txt
```

### 6. Verification
Checking if the model is loaded properly and object detection module is working right.
Run the below code:
```
python detect.py --weights "path/to/yolov9.pt" --source "path/to/your/video_or_image.jpg" --device 0
```
The yolov9.pt can be found in the readme file of the same, you need to download the weight in order to run the project. 
There are different files for the weights, based on the size of the model which is trained on the COCO dataset.

### GPU Selection
* **CUDA Device**: PyTorch (the framework YOLOv9 is built on) assigns an integer index to each available NVIDIA GPU in your system, starting from 0.
* **Single GPU**: If you have only one GPU installed, its index is 0.
* **Multi-GPU**: If you have multiple GPUs, --device 1 would target the second GPU, --device 2 the third, and so on.

### Source selection:
* **--source 0:** This tells the script to look for a local hardware camera instead of a saved file. 0 represents your computer's default integrated webcam.
* **Secondary Cameras:** If you have an external USB webcam plugged in and want to use it instead, try changing the source to 1 or 2

To fine tune the model to only detect the License Plate, you need to train the yolo model for it and get the .pt file.
Here we are using the existing trained weights for detecting the license plate.
You can download the weights from kaggle from the below link:
https://www.kaggle.com/datasets/noepinefrin/yolov9-fine-tuned-plate-detection-model-weights

While running the model use this weights.

### Reading Number Plate:
To read the number plate, we extract the text out of the lisence plate detected. Here Easy OCR is used to read the text.
```
import cv2
import torch
import easyocr
import numpy as np

for *xyxy, conf, cls in reversed(det):
                    # ---- START EASYOCR INTEGRATION ----
                    ocr_text = ""
                    if conf > 0.40: # Only run OCR on reasonably confident detections
                        try:
                            # Extract coordinates
                            xmin, ymin, xmax, ymax = int(xyxy[0]), int(xyxy[1]), int(xyxy[2]), int(xyxy[3])
                            h_img, w_img, _ = im0.shape
                            
                            # Crop the license plate from the original high-res image (im0)
                            # Adding a small 2-pixel padding safely within boundaries
                            cropped_plate = im0[max(0, ymin-2):min(h_img, ymax+2), max(0, xmin-2):min(w_img, xmax+2)]
                            
                            if cropped_plate.size > 0:
                                # Pre-process: Grayscale and Upscale by 2x for better readability
                                gray_plate = cv2.cvtColor(cropped_plate, cv2.COLOR_BGR2GRAY)
                                resized_plate = cv2.resize(gray_plate, None, fx=2, fy=2, interpolation=cv2.INTER_CUBIC)
                                
                                # Feed into EasyOCR
                                ocr_results = reader.readtext(resized_plate)
                                
                                if ocr_results:
                                    # Combine texts if it detects multiple lines/blocks inside the box
                                    ocr_text = " ".join([res[1] for res in ocr_results]).strip()
                                    LOGGER.info(f"✨ TEXT DETECTED: {ocr_text} (YOLO Conf: {conf:.2f})")
                        except Exception as e:
                            LOGGER.error(f"OCR Error: {e}")
```
This piece of the code should be put in detect.py file, and the license plate will be captured and showed in terminal