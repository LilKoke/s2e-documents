# Surface Force

## 1.  Overview

1. Functions
   
   - S2E handles air drag and Solar Radiation Pressure(SRP) as surface force disturbances since both disturbances affect spacecraft surfaces. The structure of both equations are same, but they have different coefficients. 
   - Thus, `SurfaceForce` base class provides the structure of equation and `AirDrag` and `SolarRadiation` sub classes provide specific calculation with appropriate coefficients.
   - Currently, the `SurfaceForce` class supports simple box shape spacecraft only.
     - Spacecraft should has six surfaces.
     - Self-shadowing effect is ignored.
   - For detailed description of `AirDrag` and `SolarRadiation`, please refer [Air Drag](./Spec_SurfaceForce_AirDrag.md) and [Solar Radiation Pressure](./Spec_SurfaceForce_SolarRadiation.md).
2. Related files

   - SurfaceForce.cpp, .h : The base class `SurfaceForce` is defined.
3. How to use

   - Make a sub class which Inherits the `SurfaceForce` class
   - Define `CalcCoef` function in the sub class.
   - Execute `CalcTorqueForce` in update function of the sub class.

## 2. Explanation of Algorithm

1. Constructor

   1. overview
      - Initialize structure parameters
   2. inputs and outputs
      - input
        - Position vector of each surface at the body-fixed frame
        - Area of each surface
        - Normal vector of each surface at the body-fixed frame
          - Normal vectors should be the unit vector.
      - output
        - Instance of the class
   3. algorithm: NA

   4. note: NA

2. `CalcTorqueForce` function

   1. overview

      - The main function to calculate the force and torque generated by the surface force disturbances.

   2. inputs and outputs

      - input
        - `input_b`: direction of disturbance source at the body frame
        - `item`: parameter which decide the magnitude of the disturbances (Solar flux, air density)
        - Surface information defined in the constructor
      - output
        - `force_b_`: Force at the body frame (unit: N)
        - `torque_b_` :Torque at the body frame (unit: Nm)
        - Both variables are defined in the `SimpleDisturbance` base class

   3. algorithm

      - Let us consider the following coordinate on a surface for surface force calculation
        - $`\bm{n}`$ is the normal vector of the surface
        - $`\bm{v}`$ is the direction vector of the disturbance source (sun, velocity vector)

      <img src="./figs/SurfaceForce_overview.JPG" alt="SummaryCalculationTime" style="zoom: 70%;" />

      - $`\bm{t}`$ is the direction of in-plane force. 

      ```math
      \bm{t}=\frac{\bm{v}\times\bm{n}}{|\bm{v}\times\bm{n}|}\times\bm{n}
      ```

      - Surface force and torque acting on the surface is expressed as following equation
        - $`\bm{r}_{s}`$ is the position vector of the surface
        - $`\bm{r}_{cg}`$ is the position vector of the center of mass

      ```math
      \bm{F}=-C_{n}\bm{n}+C_{t}\bm{t}\\
      \bm{T}=(\bm{r}_{s}-\bm{r}_{cg})\times\bm{F}
      ```

      - Detail of the $`C_{n}`$ and $`C_{t}`$ are defined by sub classes by using `CalcCoef` function

   4. note

      - NA


## 3. Results of verifications

 - Verifications will be done by sub classes.

## 4. References

1. 