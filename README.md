# ESP32 Micro-ROS Motor Controller (No Encoders)

This project runs a ROS2-enabled motor controller on an ESP32 using the Arduino IDE. It receives velocity commands (`cmd_vel`) from ROS2 and controls two simple DC motors (no encoders required).

## Prerequisites

**Before running this project, install micro-ROS on ESP32 using this tutorial:**  
[Complete tutorial on how to install micro-ROS on ESP32 using Arduino IDE](https://medium.com/@smilesajid14/complete-tutorial-on-how-to-install-micro-ros-on-esp32-s-using-arduino-ide-a40821d74a06)

## Hardware

- ESP32
- 2x DC motors (no encoders)
- Motor driver (e.g., L298N, L293D)
- Power supply

## Software

- Arduino IDE 3.x
- micro-ROS Arduino library
- ROS2 (Foxy/Humble/etc.)

## Steps

### 1. Upload Code to ESP32

- Open [`move.ino`](move.ino) in Arduino IDE.
- Select your ESP32 board and correct port.
- Install required libraries as per the tutorial above.
- Upload the code.

**After uploading the code, and whenever you run the micro-ROS agent or connect the ESP32, press the RESET button on the ESP32 board to ensure proper startup and connection.**

### 2. Connect ESP32 to ROS2

- Connect ESP32 to your PC via USB.
- Start the micro-ROS agent on your PC:
  ```sh
  ros2 run micro_ros_agent micro_ros_agent serial --dev /dev/ttyUSB0
  ```
  Replace `/dev/ttyUSB0` with your serial port.

**If the ESP32 does not connect immediately, press the RESET button again after starting the agent.**

### 3. Source ROS2 Workspace

Before running ROS2 commands, source your ROS2 installation:
```sh
source /opt/ros/<distro>/setup.bash
```
Replace `<distro>` with your ROS2 version (e.g., `foxy`, `humble`).

### 4. Send Velocity Commands

Run the ROS2 teleop node to control the robot:
```sh
ros2 run teleop_twist_keyboard teleop_twist_keyboard
```
This publishes to `/cmd_vel`.

### 5. List ROS2 Topics

To see active topics:
```sh
ros2 topic list
```

## Notes

- The code is designed for simple DC motors without encoders.
- Ensure serial permissions for your user (`sudo usermod -a -G dialout $USER`).
- The ESP32 will blink its LED if there is a micro-ROS error.
- Always press the RESET button after uploading code or starting the micro-ROS agent for reliable operation.

---

Main logic: [`move.ino`](move.ino)
