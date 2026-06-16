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
You can download the weights from 