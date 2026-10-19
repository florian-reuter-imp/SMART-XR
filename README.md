# SMART-XR

**Scalable Machine Automation Robotics Training in XR**

> **Status (October 2026):** this repository is being set up and currently
> contains this README and the licence only. Source code, teaching content and
> documentation follow step by step over the coming weeks. Until then the
> sections below describe the planned state, and the setup cannot be followed
> yet.

SMART-XR is a modular VR framework for robotics education in manufacturing
contexts. It takes learners from getting to know a robot, through interactive
path programming, to seeing the mathematics behind it — compliance ellipsoids,
manipulability, singularities. Robot models come from URDF, and the teaching
content lives in JSON, separate from the application logic.

Developed at the Institute of Materials and Processes (IMP), Karlsruhe
University of Applied Sciences (HKA), funded through Open Call 2 of the EU
project **MASTER** (see [Acknowledgment](#acknowledgment)).

## What it does

- **Three teaching scenes:** robot catalogue, robot programming, and the
  mathematical–physical background
- **Teaching Content System (TCS):** chapters are JSON files, sequenced by a
  state machine. Content can be edited, extended and translated without
  touching code. The course exists in German and English.
- **Own kinematics:** closed-form inverse kinematics for ortho-parallel
  six-axis robots (OPW), a numeric solver for arbitrary serial chains, a
  five-axis projection, Jacobian, Cartesian compliance, manipulability and
  singularity classification — plain C#, no dependencies, with tests
- **Robot library:** 229 robots from a URDF dataset; 80 of them solve in
  closed form
- **ROS 2 and MoveIt:** a Docker stack plans and executes motions; behaviour
  trees (BehaviorTree.CPP) drive the sequences
- **OpenXR:** no vendor lock-in. Developed and tested on a Meta Quest 3.
- **Standalone:** a regular Unity application, no separate deployment platform

## Feature modules

Features are packaged so that a single one can be taken over on its own — code,
prefab, teaching chapter and tests together, with a parts list stating what it
requires and which render pipelines, Unity versions and XR setups it accepts.
A checking tool verifies that a module is self-contained by building it in a
freshly created, empty Unity project.

Two modules are finished:

| Module | Shows | Requires |
|---|---|---|
| Compliance | compliance ellipsoid at the tool point | kinematics package; TCS optional |
| Jacobian | velocity ellipsoid, manipulability, singularity kind | kinematics package; TCS optional |

## Requirements

- **Unity 6000.3.11f1.** Developed and tested with this version. The
  kinematics package itself declares 2022.3 and uses no newer API.
- An **OpenXR**-capable headset, or the XR Interaction Simulator for desktop
  work. Tested on Meta Quest 3 over Link; a standalone Android build is
  configured but not yet validated on device.
- **Docker**, for the ROS 2 part only.
- **realvirtual Starter** — optional, but recommended. A free Unity Asset
  Store package for industrial automation: it contributes drive components and
  an example manufacturing cell, which makes the teaching scenes considerably
  closer to a real production environment. SMART-XR integrates with it where
  that helps. The feature modules and the kinematics package do not depend on
  it. Its licence does not permit redistribution, so it is not part of this
  repository.

## Getting started

*Applies once the code is published.*

```powershell
git clone https://github.com/florian-reuter-imp/SMART-XR.git
cd SMART-XR
.\setup.ps1
```

`setup.ps1` fetches what this repository deliberately does not contain — the
URDF robot dataset — and reports what it cannot fetch itself, such as packages
that have to come from the Unity Asset Store.

The ROS 2 stack is a Docker Compose setup. Its published ports bind to
localhost by default: the Unity endpoint and the container desktop have no
authentication of their own.

## Project history

SMART-XR was built within the MASTER project, which required the
[VIROO](https://virooportal.virtualwareco.com/) platform for deployment and
realvirtual Professional for kinematics and manufacturing cells. The paper
below describes that setup. Since the project ended, both dependencies have
been removed: SMART-XR runs as a standalone Unity application, and kinematics
and interaction are its own.

## Roadmap

| Item | Status |
|---|---|
| Standalone build without VIROO | done |
| Replace realvirtual Professional with own modules | done |
| Kinematics as a reusable package, with tests | done |
| Feature modules with declared, verified compatibility | two done, more to follow |
| ROS 2 / MoveIt with behaviour trees, simulated | done |
| ROS 2 to a physical low-cost arm (LeRobot SO-101) | planned |
| Structured learning analytics (e.g. xAPI) | planned |

## Related publication

F. Reuter, K. Maass, M. Kipfmüller, F. Bellalouna, "SMART-XR: A Modular VR
Framework for Scalable Robotics Training in Manufacturing," presented at IEEE
MetroXRAINE 2026, Chemnitz, Germany, 21 October 2026. DOI to be added upon
publication.

## Acknowledgment

<img src="eu-emblem.svg" alt="European Union emblem" height="60">

**Co-funded by the European Union.**

SMART-XR was awarded funding through **Open Call 2** of the MASTER project
— *Mixed reality ecosystem for teaching robotics in manufacturing*,
[master-xr.eu](https://master-xr.eu/). MASTER has received funding from the
European Union's Horizon Europe research and innovation programme under grant
agreement No 101093079.

Views and opinions expressed are however those of the author(s) only and do
not necessarily reflect those of the European Union or the European
Commission. Neither the European Union nor the granting authority can be held
responsible for them.

## Licence

**Code: Apache License 2.0** — see [LICENSE](LICENSE).

**Teaching content: CC BY 4.0.** The JSON course chapters are texts, not
software; a Creative Commons licence states more clearly that lecturers may
use, adapt and translate them. The boundary is documented with the content.

### Third-party components

They keep their own licences, and a NOTICE file will list all of them. The ones
worth naming here already:

| Component | Licence | By |
|---|---|---|
| [urdf_files_dataset](https://github.com/Daniella1/urdf_files_dataset) | MIT | Daniella Tola |
| [ros_tcp_endpoint](https://github.com/Unity-Technologies/ROS-TCP-Connector) | Apache-2.0 | Unity Technologies |
| [Flange](https://github.com/Preliy/Flange) | BSD 3-Clause | Preliy |
| [BehaviorTree.CPP](https://github.com/BehaviorTree/BehaviorTree.CPP) | MIT | Davide Faconti |

The robot models inside the URDF dataset carry their own licences from their
manufacturers and maintainers; the dataset ships those files alongside the
models.

The closed-form kinematics follows the OPW parametrisation of Brandstötter,
Angerer and Hofbaur (Austrian Robotics Workshop 2014). The implementation here
is independent of any existing one and follows the derivation in that paper.
