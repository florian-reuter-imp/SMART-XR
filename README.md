# SMART-XR

**Scalable Machine Automation Robotics Training in XR**

SMART-XR is a modular VR framework for robotics education and training in manufacturing contexts. It guides learners from robot familiarization through interactive path programming to the visualization of mathematical fundamentals (forward/inverse kinematics, Jacobian-derived stiffness ellipsoids), using URDF-based robot models and a JSON-driven Teaching Content System (TCS) that separates instructional content from application logic.

The project is developed at the Institute of Materials and Processes, Karlsruhe University of Applied Sciences, within the European **MASTER-XR** ecosystem (Horizon Europe, Open Call 2).

> **Status:** Work in progress. The framework is under active development; interfaces, scene content, and dependencies may still change.

## Features

- **Three educational scenes** — robot familiarization, interactive path programming, and visualization of mathematical fundamentals (Jacobian-based stiffness ellipsoids)
- **Teaching Content System (TCS)** — instructional content is stored in JSON files and managed by a state machine, so content can be edited, extended, or translated without touching source code
- **URDF-based robot loading** — robot models are robot-agnostic and can be swapped without reimplementation
- **OpenXR** — hardware-independent VR interaction, not tied to a specific headset

## Requirements

- **Unity** 6000.2.7f2 (or later 6000.2.x)
- **realvirtual Starter** — required as an additional asset for kinematics/manufacturing-cell content; not included in this repository and must be imported separately (see [realvirtual.io](https://realvirtual.io))
- A compatible OpenXR-capable VR headset (developed and tested with Meta Quest 3)

> Note: an earlier version of the project used [VIROO](https://virooportal.virtualwareco.com/) for content delivery. VIROO has since been removed from this project; the framework now runs as a standalone Unity application.

## Getting started

1. Clone this repository.
2. Open the project in Unity 6000.2.7f2 (or later).
3. Import **realvirtual Starter** into the project via the Unity Asset Store / Package Manager.
4. Open the desired scene and press Play (with an OpenXR headset connected) or use the in-editor XR simulator.

*(Detailed setup instructions will follow as the project stabilizes.)*

## Roadmap

- [ ] Finalize Scene 3 (mathematical fundamentals)
- [ ] Reduce dependency on proprietary components
- [ ] ROS2/MoveIt integration for connecting virtual and physical robots
- [ ] Public release of open framework components (TCS architecture, URDF configurations, scene descriptions)

## Related publication

This repository accompanies the paper:

F. Reuter, K. Maass, M. Kipfmüller, F. Bellalouna, "SMART-XR: A Modular VR Framework for Scalable Robotics Training in Manufacturing" *(paper details / DOI to be added upon publication)*.

## Acknowledgment

This work has received funding from the European Union's Horizon Europe programme under the MASTER XR project (Open Call 2).

## License

This project is licensed under the GNU General Public License v3.0 — see [LICENSE](./LICENSE) for details.
