# AhaRobot Firmware Resources

<div align="center">
  <img src="assets/logo.png" alt="AhaRobot Logo" width="200"/>
</div>

<div align="center">
  <a href="https://aha-robot.github.io/" target="_blank">Project Website</a> • 
  <a href="https://arxiv.org/abs/2503.10070" target="_blank">Paper</a> • 
  <a href="https://www.notion.so/1b433900bc8780c4a503e3490ce3e718?pvs=21" target="_blank">Documentation</a> • 
  <a href="https://github.com/hilookas/astra_ws" target="_blank">ROS Code</a> •
  <a href="https://github.com/hilookas/AstraFirmwares" target="_blank">Firmware Code</a> •
  <a href="https://github.com/hilookas/Astra_Hardwares" target="_blank">Hardware Code</a> •
  <a href="https://huggingface.co/lookas" target="_blank">Dataset</a>
</div>

## Repository Contents

This repository contains firmware resources for AhaRobot, organized as follows:

### Main Components

#### Robot Body Controllers
- **AstraArmController**: Arm controller firmware
  - Controls the arm movements of the Astra robot

- **AstraLiftController**: Lift controller firmware
  - Controls the robot's lifting mechanism

- **AstraHeadController**: Head controller firmware
  - Controls the robot's head movements and expressions

#### Teleoperation Controllers  
- **AstraPedalController**: Teleoperation controller firmware
  - Controls and communicates with the teleoperation handle

## How-to-use

For detailed documentation, please refer to the following resources:

- [Getting Started Guide](docs/getting_started.md)
- [Hardware Assembly Guide](docs/hardware_assembly.md)
- [Flashing Firmware](docs/firmware_flashing.md)
  - Flashing Lift Controller
  - Testing Lift Controller
  - Flashing Arm Controller
  - Calibrating Centor Point of Joints
  - Testing Two Arms
  - Configuring ODrive

## License

This project is licensed under the [GNU General Public License v3.0 (GPL-3.0)](https://www.gnu.org/licenses/gpl-3.0.en.html) with additional restrictions.

This means:
- ✅ You are free to use, modify and distribute the source code
- ✅ You must make your modifications available under the same license
- ✅ You must state changes made to the code
- ✅ You must include the original copyright notice
- ❌ You may not use the material for commercial purposes
- ❌ Modifications must also prohibit commercial use

IMPORTANT: This project explicitly prohibits ANY commercial use, including but not limited to selling products based on this project.

See the [LICENSE](LICENSE) file for the full license text.