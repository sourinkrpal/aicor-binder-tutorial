# Creating Your First Lab
### Draft by Sourin Kumar Pal

The **Virtual Research Building (VRB)** is a cloud-based platform for running reproducible robotic experiments inside browser-based virtual labs.

This tutorial explains:
- what a virtual lab is,
- how to add your own robot model,
- how to visualize the robot inside the lab, and
- how to integrate your preferred programming tools (or the VRB’s tools) to control it.

---

## 1. What is a Virtual Lab?

### 1.1 Brief Overview

A **virtual lab** is a version-controlled, self-contained robotics workspace packaged as a **Docker container**.  
It includes all components required for an experiment:

- robot model  
- environment model  
- simulation or control software  
- your code and data  
- any additional libraries you install  

Because the entire lab exists inside a portable Docker image and is connected to Git, anyone can launch it in the exact same state that allows repeatable, shareable robotics experiments.

---

### 1.2 Technical Overview

A VRB lab runs through a set of virtualization and web technologies that work together:

- **Docker** provides an isolated environment with all your dependencies and robot models.  
- **Git** tracks your lab’s content and connects it to cloud execution services.  
- **Binder** builds and launches your Docker image directly in the browser.  
- **JupyterLab** offers a browser-based development environment for editing and running code.  
- **VNC** gives you access to a full desktop session in the browser, for example to run GUIs such as simulators.

Together, these systems allow you to edit, run, visualize, and share robotics experiments entirely online, without installing any robotics toolchain locally.

---

## 2. What’s in the Box?

The VRB base image already includes a few core tools so you can start working right away.

### 2.1 Preinstalled Tools

- **ROS**  
  The standard middleware used in robotics for communication and running robot software.

- **JupyterLab**  
  The main web interface you see in the browser. You can browse files, open terminals, and run notebooks here.

- **VSCode Server**  
  A browser-based version of Visual Studio Code. It lets you edit your lab with a full IDE without installing anything locally.

- **VNC Desktop**  
  A virtual Linux desktop environment inside the browser. Useful for running GUI tools, simulators, and robot viewers.

---

### 2.2 Installing More Software

If you need extra libraries or tools, you can simply add them to the lab’s `Dockerfile`.  
When Binder rebuilds your lab, those tools will be included automatically.

Typical things you can add:
- Physics engines (MuJoCo, Bullet etc.)
- Scene/robot management libraries (Multiverse)
- Perception frameworks (RoboKudo)
- Robot control frameworks (PyCRAM, MoveIt)
- Full ROS 2 distributions
- Data science libraries (NumPy, PyTorch, TensorFlow)

---

### 2.3 Example: Installing a Python Package

Below is a minimal example showing how to install `numpy` inside your lab's Dockerfile:

```Dockerfile
# Install Python packages
RUN pip install numpy
```

When you commit and push the updated Dockerfile, Binder will rebuild the lab with `numpy` included.