# OpenFOAM 6DOF Sphere Simulation Case

## Project Overview

This project demonstrates a **6 Degrees of Freedom (6DOF)** simulation case using **OpenFOAM 2406**, where a sphere moves freely in an XY-plane under predefined constraints. It uses the **`sixDoFRigidBodyMotion`** solver to calculate the dynamic response of a rigid body (the sphere) to fluid forces and torques.

---
## Purpose

This project demonstrates a **6 Degrees of Freedom (6DOF)** simulation case using **OpenFOAM 2406**. It provides a practical example for simulating the motion of a rigid body (a sphere) under fluid forces and torques in the XY-plane. The goals of this project include:

- **Education and Research**: Useful for demonstrating fluid dynamics and aerodynamics concepts in academic settings.
- **Industrial Applications**: Helps analyze the fluid-structure interaction of freely moving objects, applicable to industries such as marine, aerospace, and automotive.
- **Open Source Learning**: Offers a detailed, reproducible case study for both beginners and advanced users to explore OpenFOAM capabilities.

---

## Prerequisites

### Required Software
1. **OpenFOAM 2406**
   - [Download OpenFOAM](https://www.openfoam.com/news/main-news/openfoam-v2406)
   - Source the environment before running


2. **MPI (Message Passing Interface)**
For parallel computations, this project uses OpenMPI, which is often the default MPI library for OpenFOAM installations. Ensure that OpenMPI is installed and correctly configured.

 Steps to Check or Install OpenMPI:
   Run the following command in the terminal:
  ```bash
   mpirun --version
  ```
   If the command outputs an OpenMPI version, it is already installed.

---


### Recommended Hardware
- **Operating System**: Linux (Ubuntu 20.04 or later recommended)
- **CPU**: Multi-core processor
- **Memory**: 16GB or more
- **Disk Space**: At least 20GB of free space for storing simulation results

---

## Features

- **6DOF Dynamics**: The sphere's motion includes translation and rotation with predefined constraints.
- **Velocity Constraints**:
  - Initial velocity: $x = 10 \, \mathrm{m/s}, y = 10 \, \mathrm{m/s}, z = 0 \, \mathrm{m/s}$.
  - The sphere is restricted to motion within the XY-plane (Z-axis translation and rotation disabled).
- **Dynamic Mesh**: Using the `sixDoFRigidBodyMotion` solver, the mesh dynamically adjusts based on the sphere's motion.
- **Parallel Execution**: Pre-configured for 8-core parallel computation.
- **Simulation Details**:
  - Solver: `overPimpleDyMFoam` (used for single-phase incompressible fluid ).
  - Default setup configured for 8 cores (parallel execution).
- **Output Data**:
  - Forces and torques acting on the sphere.
  - Drag, lift, and moment coefficients (`coefficient.dat`).
  - Velocity and pressure fields.

---

## Installation and Prerequisites

- **OpenFOAM Version**: OpenFOAM 2406  
  Ensure the environment is sourced:
  ```bash
  source /you/path/OpenFOAM/OpenFOAM-2406/etc/bashrc
  System: Linux (recommended: Ubuntu 20.04 or later)
   ```


## Directory Structure

```plaintext
.
├── 0
│   ├── U
│   ├── epsilon
│   ├── include
│   │   ├── fixedInlet
│   │   ├── frontBackUpperPatches
│   │   └── initialConditions
│   ├── k
│   ├── motionScale
│   ├── nuTilda
│   ├── nut
│   ├── omega
│   ├── p
│   ├── pointDisplacement
│   ├── rho
│   └── zoneID
├── constant
│   ├── dynamicMeshDict
│   ├── extendedFeatureEdgeMesh
│   │   ├── sphere15.extendedFeatureEdgeMesh
│   │   ├── sphere15_concaveFeaturePts.obj
│   │   ├── sphere15_convexFeaturePts.obj
│   │   ├── sphere15_edgeDirections.obj
│   │   ├── sphere15_edgeMesh.obj
│   │   ├── sphere15_externalEdges.obj
│   │   ├── sphere15_flatEdges.obj
│   │   ├── sphere15_internalEdges.obj
│   │   ├── sphere15_mixedFeaturePts.obj
│   │   ├── sphere15_mixedFeaturePtsStructure.obj
│   │   ├── sphere15_multipleEdges.obj
│   │   ├── sphere15_openEdges.obj
│   │   └── sphere15_regionEdges.obj
│   ├── polyMesh
│   │   ├── boundary
│   │   ├── boundary:Zone.Identifier
│   │   ├── cellZones
│   │   ├── cellZones:Zone.Identifier
│   │   ├── faceZones
│   │   ├── faceZones:Zone.Identifier
│   │   ├── faces
│   │   ├── faces:Zone.Identifier
│   │   ├── neighbour
│   │   ├── neighbour:Zone.Identifier
│   │   ├── owner
│   │   ├── owner:Zone.Identifier
│   │   ├── pointZones
│   │   ├── pointZones:Zone.Identifier
│   │   ├── points
│   │   └── points:Zone.Identifier
│   ├── polyMesh1
│   │   ├── boundary
│   │   ├── faces
│   │   ├── neighbour
│   │   ├── owner
│   │   └── points
│   ├── transportProperties
│   ├── triSurface
│   │   ├── sphere.stl
│   │   └── sphere15.stl:Zone.Identifier
│   └── turbulenceProperties
└── system
│   ├── blockMeshDict
│   ├── controlDict
│   ├── decomposeParDict
│   ├── fvSchemes
│   ├── fvSolution
│   ├── meshQualityDict
│   ├── setFieldsDict
│   ├── snappyHexMeshDict
│   ├── surfaceFeatureExtractDict
│   └── topoSetDict
├── README.md           # Project description
└──LINCESE

```

## Usage Instructions
1. **Modify the Mesh**:
  - **⚠ Important:**
  - **The current mesh has already been generated using `snappyHexMesh`.**

- **If you are a beginner and only aim to simulate the motion** of the sphere in a **two-dimensional context**, it is highly recommended **`not to modify this configuration`**. The current setup is specifically designed for a 6DOF simulation, with mesh parameters and constraints optimized for accurate and stable results.

  Switching to a simplified 2D simulation requires:
  - Reconfiguring the mesh generation process.
  - Adjusting domain boundaries.
  - Modifying solver and constraint settings.

  These changes can introduce unintended errors or instability, especially if you are unfamiliar with OpenFOAM’s mesh generation and configuration processes. 

  **Recommendation for Beginners:**
  - Use the provided 3D setup and focus on restricting the sphere’s motion to the **XY-plane** by adjusting the constraints in `dynamicMeshDict`. This approach avoids unnecessary complexity while still yielding valid results for 2D motion.
  -  Avoid regenerating the mesh unless absolutely necessary. If required, ensure you understand the changes in `blockMeshDict` and `snappyHexMeshDict`.

  By using the provided configuration, you can concentrate on understanding the simulation dynamics and analyzing results without facing potential setup issues. Advanced modifications can be explored once you gain more experience.

   - **If you do not wish to modify the mesh**, you can skip the regeneration step and directly run the following command to decompose the mesh for parallel execution：
     ```bash
     decomposePar
     ```
   - **If you wish to regenerate the mesh**, delete the `polyMesh` directory in `constant` and rename `polyMesh1` to `polyMesh`. Then, run the following commands to regenerate the mesh:
     ```bash
     blockMesh
     snappyHexMesh
     ```

2. **Adjust Initial Conditions**:
   - The initial settings for the sphere, such as velocity, angular velocity, and motion constraints, can be modified in `constant/dynamicMeshDict`.

  **For example**:
  1. Changing Initial Velocity:
   To change the initial velocity of the sphere, locate the `sixDoFRigidBodyMotionCoeffs` section in `dynamicMeshDict` and modify the `velocity` parameter.
   For instance, change:
   `velocity (10 10 0);`
   to:
   `velocity (15 15 0);`

  2. Modifying Motion Constraints in the XY-plane:
   To change the sphere's movement constraints within the XY-plane, update the `constraints` section. Specifically, adjust the `fixedPlane` settings to define the desired constraints.

  3. Changing Rotational Constraints:
   To modify the sphere's rotational behavior, edit the `fixedAxis` settings under the `constraints` section. Apply the appropriate rotational constraints based on your requirements.

  By customizing these parameters, you can precisely control the sphere's initial conditions and motion behavior.


3. **Modify Simulation Time**:
   - The default simulation time is set to 2.5 seconds. To change this, update the corresponding settings in `system/controlDict`.

4. **Current Setup**:
   - The flow conditions are configured for free flow around the sphere.
   - The pressure and velocity on the sphere surface are calculated in real-time.
   - The simulation uses the k-Omega turbulence model. To modify this, navigate to the `0` directory and edit the appropriate files.
5. **Adjusting for More Cores**:
   - If you want to run the simulation on more or fewer cores:
   - `numberOfSubdomains 4;  # For 4 core`
   - Edit the `system/decomposeParDict` file and update numberOfSubdomains to the desired number of cores.
---

## Usage:
  1. Run the mesh decomposition:
     ```bash
     decomposePar
     ```
  2. Run the simulation in parallel:
     ```bash
     mpirun -np 8 overPimpleDyMFoam -parallel
     ```
  3. Merge the decomposed mesh and results: After the simulation is complete, merge the decomposed mesh and field data for post-processing:
     ```bash
     reconstructPar
     ```

## Author
- Name: JIANG BIQI 
- Email:   2595762879a@gmail.com  
- GitHub: [JIANGBIQI2003](https://github.com/JIANGBIQI2003)

## License

This project is licensed under the GNU General Public License v3.0.  
See the [LICENSE](./LICENSE) file for details.

For more information about the GPL, visit [GNU Licenses](https://www.gnu.org/licenses/gpl-3.0.en.html).
