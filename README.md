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
Checking if the model is loaded properly and object detection module is working good