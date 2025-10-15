# **🚀 XRoboToolKit Quick Start Guide**

XRoboToolKit is a cross-platform framework for **XR-based robot teleoperation**, **training data collection**, and **AR-assisted task execution**. For arm64 version(Nvidia orin) please check this tutorial.  
 It includes:

* 🧠 **XRoboToolkit-PC-Service** — The main host application that connects XR headset and robot.

* 🪶 **xrobotoolkit\_sdk** — Python SDK (PyBind wrapper) for communication with PC-Service.

* 🕶 **XRoboToolkit-Headset-App** — Unity-based XR client for Pico headset.

* 🤖 **XRoboToolkit-Teleop-Sample-Python** — Example Python teleoperation and simulation scripts.

---

## **🧩 Prerequisites**

Before starting, make sure you have the following:

| Component | Description |
| ----- | ----- |
| **Conda** | Python environment manager (used to run teleop sample) |
| **ADB** | Android Debug Bridge (used to install XR headset app) |
| **Network** | Headset and PC should be on the same local network for automatic IP matching. You can also manually type the IP in the XR application |
| **Robot SDK** | Installed or simulated robot environment (optional for testing) |

---

## **X86 PC Installation(Ubuntu and Windows supported)**

### **1️⃣ Install XRoboToolkit-PC-Service**

**for Ubuntu 22.04 user:**

You can either download the `.deb` package or build from source.

`‘’’`  
`# Install prebuilt package`  
`sudo dpkg -i XRoboToolkit-PC-Service_1.0.0_ubuntu_22.04_amd64.deb`  
`‘’’`

💡 The service will be installed under `/opt/apps/roboticsservice/`.

To start the service manually:

`cd /opt/apps/roboticsservice`  
`bash runService.sh`

Or double-click the app icon `XRoboToolkit-PC-Service` from the desktop menu.

**For Windows user**

You can either download the [XRoboToolkit-PC-Service.win.zip](https://github.com/XR-Robotics/XRoboToolkit-PC-Service/releases/download/v1.0.0/XRoboToolkit-PC-Service.win.zip) or build from source.

after you extract the file, double click the run3D.exe file in the folder

 

---

### **2️⃣ Clone and Set Up Teleoperation Python Sample**

`# Clone the sample repository`  
`git clone https://github.com/XR-Robotics/XRoboToolkit-Teleop-Sample-Python.git`  
`cd XRoboToolkit-Teleop-Sample-Python`

`# Create and activate conda environment`  
`conda create -n xrobotoolkit python=3.10 -y`  
`conda activate xrobotoolkit`

`# Install dependencies`  
`bash setup_conda.sh --install`

⚙️ This package communicates with PC-Service via the `xrobotoolkit_sdk` Python module. (Both ubuntu and windows can try the teleoperation, simulation, and real robot demo)

---

### **3️⃣ Install XR App on Pico 4 Ultra Headset**

1. Enable **Developer Mode** on the Pico 4 Ultra headset if you are using brand new device. You may need to register the pico account for the first time. This is only for video recording and live casting features in the headset.

    (See official Pico developer documentation for enabling developer mode.)

Connect the headset via USB and verify with:

 `adb devices`

2. 

Install the XR App:

   
`‘’’`  
`adb install -g XRoboToolkit-PICO-1.1.1.apk`  
`‘’’`

---

### **4️⃣ Run the Sample**

1. On PC double click the run3D.exe (windows) in the zip file or click XRoboToolkit-PC-Service (ubuntu). The unity based visualization app will start.  
     
   for ubuntu user, you can also use terminal to start the app (no visualization will show)  
   `cd /opt/apps/roboticsservice`  
   `bash runService.sh`  
   

2. On the Pico headset, open the **XRoboToolkit** app. the application can be find in Library-\>unknown (note unknown is located in the right side). Connect the PC and start sending the data. visualization app on PC will reflect the head and controller.  
3. check your environment(optional)  
   conda activate `xrobotoolkit`  
   `git clone https://github.com/XR-Robotics/XRoboToolkit-PC-Service-Pybind`  
   `cd XRoboToolkit-PC-Service-Pybind`

`python examples/run_teleop_sample.py`

if you find the data is not all zero, the environment is ready to use 

4. try teleoperation on UR5 mujoco simulation. make sure you are in `XRoboToolkit-Teleop-Sample-Python`  
   python scripts/simulation/teleop\_dual\_ur5e\_mujoco.py  
   

