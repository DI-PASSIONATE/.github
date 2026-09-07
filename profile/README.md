# DI-PASSIONATE

**An open-source design and simulation environment for highly integrated 2.5D/3D chip systems.**

Modern high-performance systems are built by combining heterogeneous chiplets into a
single package. The design tools for that packaging step are largely proprietary.
DI-PASSIONATE is a publicly funded research project building a *free* design environment
for the packages of integrated multi-chip systems - from 3D structure modelling and
electrical/thermal simulation through to automated, goal-driven optimization, using only
open-source tools.

The approach is demonstrated on two very different subsystems: a digital accelerator and
an analog power amplifier.

---

## Repositories

| Repository | What it does |
| --- | --- |
| **[ORCA](https://github.com/DI-PASSIONATE/ORCA)** | *Open RF Integrated Circuit Automation.* Simulates RFIC geometries with open-source EM tools and trains AI/ML surrogate models that predict S-parameters for a given geometry in milliseconds instead of hours. |
| **[COBRA](https://github.com/DI-PASSIONATE/COBRA)** | *A Circuit-Level Open-Source Based RFIC AI-Assisted Optimizer.* Loads ORCA's surrogate models, runs circuit-level SPICE simulation via Xyce, and optimizes a design against user-defined goals; with optional full-wave EM fine-tuning in AWS Palace. |

## Built on open source

The toolchain deliberately depends only on tools anyone can install:
[Xyce](https://xyce.sandia.gov/) (SPICE simulation), [Qucs-S](https://ra3xdh.github.io/)
(schematic capture and netlists), [gds2palace](https://github.com/VolkerMuehlhaus/gds2palace_ihp_sg13g2) (GDS to Palace conversion), [AWS Palace](https://awslabs.github.io/palace/)
(full-wave EM), [gmsh](https://gmsh.info/) (meshing), [ONNX
Runtime](https://onnxruntime.ai/) (surrogate inference),
[Optuna](https://optuna.org/) (optimization) and
[scikit-rf](https://scikit-rf.org/) (RF network handling).

## Getting started

Start with [COBRA](https://github.com/DI-PASSIONATE/COBRA) if you want to optimize a
circuit, or with [ORCA](https://github.com/DI-PASSIONATE/ORCA) if you want to build a
surrogate model for your own geometry. COBRA's
[documentation](https://di-passionate.github.io/COBRA/) covers installation, the
configuration format, the GUI and the scripting API.

Questions, bug reports and feature ideas belong in the issue tracker of the repository
they concern. See [CONTRIBUTING.md](https://github.com/DI-PASSIONATE/.github/blob/main/CONTRIBUTING.md)
before opening a pull request, and [SECURITY.md](https://github.com/DI-PASSIONATE/.github/blob/main/SECURITY.md)
for reporting a vulnerability.

## Project and funding

DI-PASSIONATE (*Open-Source-Entwurfs- und Simulationsumgebung für hoch-integrierte
2.5D/3D-Chipsysteme*) runs from **May 2024 to April 2027** and is coordinated by
**Friedrich-Alexander-Universität Erlangen-Nürnberg (FAU)**.

It is funded by the German Federal Ministry of Research, Technology and Space
(Bundesministerium für Forschung, Technologie und Raumfahrt, BMFTR - formerly BMBF)
within the programme *Design-Instrumente für souveräne Chipentwicklung mit Open-Source*
(**DE:Sign**), with €1.16 million in funding plus a project allowance for the
participating universities.

More about the project: [elektronikforschung.de](https://www.elektronikforschung.de/projekte/di-passionate)
· [DE:Sign programme](https://www.elektronikforschung.de/foerderung/bekanntmachungen/design)
