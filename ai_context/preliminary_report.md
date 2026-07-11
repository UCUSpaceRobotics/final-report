## European Rover Challenge 2026

# Preliminary Report

## UCU Space Robotics

## Indomitus

```
Affiliation: Ukrainian Catholic University
Submission date: April 8, 2026
Revision: 1.
```

## Contents


- 1 Matrix of Compliance
- 2 Preliminary Test Plan
   - 2.1 Test Timeline
   - 2.2 Test Descriptions
- 3 Preliminary Design Description
   - 3.1 Product Trees / Physical Breakdown Structures
      - 3.1.1 Rover Product Tree / Physical Breakdown Structure
      - 3.1.2 Drone Product Tree / Physical Breakdown Structure
      - 3.1.3 System Architecture Wiring Diagram
   - 3.2 Rover Design Description
      - 3.2.1 Mechanical Design
         - 3.2.1.1 Chassis Configuration and Geometry
         - 3.2.1.2 Drive Calculation and Selection
         - 3.2.1.3 Wheel Design
         - 3.2.1.4 Manipulator Configuration and Kinematics
         - 3.2.1.5 Load Analysis and Selection of Manipulator Actuators
         - 3.2.1.6 End-Effector Design
         - 3.2.1.7 Sample Storage and Weighing System
      - 3.2.2 Electrical Power Subsystem
         - 3.2.2.1 Battery Configuration and Hot-Swap Design
         - 3.2.2.2 Power Distribution and Regulation
      - 3.2.3 Communication Subsystem
         - 3.2.3.1 Communication Architecture Overview
         - 3.2.3.2 Frequency Plan
         - 3.2.3.3 Link Performance Analysis
         - 3.2.3.4 Bandwidth Management
         - 3.2.3.5 Communication Redundancy
      - 3.2.4 On-Board Sensor and Imaging Systems
         - 3.2.4.1 Navigation Sensor Suite
         - 3.2.4.2 Science Sensor Suite
         - 3.2.4.3 Rover Camera Suite
      - 3.2.5 Software Architecture
         - 3.2.5.1 State Estimation and Localization
         - 3.2.5.2 Autonomous Navigation and Collision Avoidance
         - 3.2.5.3 Arm Kinematics and Motion Planning
         - 3.2.5.4 Science Autonomous Operation Architecture
      - 3.2.6 Operations
         - 3.2.6.1 Ground Station Setup and Equipment
         - 3.2.6.2 Teleoperation and Control Interface
   - 3.3 Rover Technical Budgets
      - 3.3.1 Mass Budget and Per-Task Configuration Breakdown
      - 3.3.2 CoG Analysis and Slope Stability
      - 3.3.3 Power Budget
      - 3.3.4 Data Link Budget
   - 3.4 Rover Safety Systems
      - 3.4.1 Emergency Stop System
      - 3.4.2 Motion Warning and Delay System
      - 3.4.3 Human Detection Safety System
   - 3.5 Drone Design Description
      - 3.5.1 Physical Design and Environmental Resilience
         - 3.5.1.1 Drone Overview
         - 3.5.1.2 Rover-Mounted Landing Platform
      - 3.5.2 Avionics and Communications Infrastructure
         - 3.5.2.1 Core Computing and Flight Control
         - 3.5.2.2 Radio Frequency Architecture
         - 3.5.2.3 System Redundancy
      - 3.5.3 Perception and Autonomous Navigation
         - 3.5.3.1 Autonomous Navigation Pipeline
         - 3.5.3.2 Localization
         - 3.5.3.3 Computer Vision and Imagery
   - 3.6 Drone Technical Budgets
      - 3.6.1 Drone Mass Budget
      - 3.6.2 Drone Power Budget
   - 3.7 Drone Safety Systems
      - 3.7.1 Failsafe Protocols
- 4 RIO Analysis
   - 4.1 Methodology
   - 4.2 Qualitative Risks Assessment, Opportunities, and Issues
- 5 Project Budget
   - 5.1 Budget Summary
   - 5.2 COTS and Custom Components
   - 5.3 Non-Engineering Costs
   - 5.4 Budget Analysis
- Appendices


## 1 Matrix of Compliance

Table 1 present a compact summary of compliance status.

```
Table 1: Compliance status and test overview summary
Compliance Status
Status Count
Compliant ( C ) 72
Partially Compliant ( PC ) 0
Non-Compliant ( NC ) 0
Not Applicable ( N/A ) 0
Total requirements 72
```
```
Test Overview
Team Count
Suspension 4
Arm 3
Science 11
Navigation 6
Electronics 3
Ground Station 3
Drone 7
Total tests 37
```
## 2 Preliminary Test Plan

Table 1 and Table 2 summarise the verification campaign. All tests listed in this section are currently
planned; execution status and results are omitted at this stage.

### 2.1 Test Timeline

```
Table 2: Test timeline (quarters / months)
```
```
Team Mar Apr May Jun Jul Aug Sep
Suspension
Electronics
Arm
Science
Navigation
Ground station
```
### 2.2 Test Descriptions

The full detailed test plan is provided in the appendices (Table 24).

## 3 Preliminary Design Description

### 3.1 Product Trees / Physical Breakdown Structures

#### 3.1.1 Rover Product Tree / Physical Breakdown Structure

Figure 16 presents the rover as a hierarchical physical breakdown: system→subsystem→assembly. The
first level separates the Main Computer, Chassis, Arm, Science, and Operation subsystems; lower levels
show the hardware modules integrated under each branch. This structure defines ownership boundaries
and supports mass budgeting, integration planning, and test coverage.

#### 3.1.2 Drone Product Tree / Physical Breakdown Structure

The physical architecture and hardware modules of the drone are illustrated in Figure 15. Functionally,
the drone operates on a distributed control hierarchy that separates high-level autonomous processing
from low-level flight stabilization. Detailed component specifications and subsystem capabilities are
expanded upon in § 3.5.1.1.

#### 3.1.3 System Architecture Wiring Diagram

The Rover consists of the following subsystems:

- **Main Computer** — performs high-level processing and collects sensor data, primarily via USB.
- **Chassis Subsystem** — drives the wheels and communicates with the main computer over CAN via the
    Chassis Controller.
- **Arm Subsystem** — controls actuators, sensors, and the arm context camera, communicating with the
    main computer via Ethernet and CAN through the Arm Controller.
- **Science Subsystems** — include sampling/deep sampling, astrobiology, and exploration (spectral and
    thermal scientific cameras).
- **Operation Subsystem** — provides external communication through two channels: Wi-Fi and a UART-
    based fallback antenna.

A detailed wiring diagram is shown in Figure 1.


```
Navigation subsystem
```
```
Chassis subsystem
```
```
Arm subsystem
```
```
Operation subsystem
```
```
Arm/Science(astrobio) subsystem
Arm/Science(sampling/deep sanpling) subsystem
```
```
Science(exploration) subsystem
```
```
USB Hub
```
```
UART-to-USB Bridge
```
```
UART-to-USB Bridge
```
```
LiDAR
```
```
Human presence sensor x
```
```
ToF Camera x
```
```
Stereo Camera
```
```
Main computer
```
```
ControllerChassis
```
```
Drive Motor x4 Rotation Motor x
```
```
Arm controller
```
```
High-torqueplanetary
actuator (q1-q3)
orientationCompact
actuator (q4-q6)
```
```
USB
```
```
USB
```
```
USB
USB
```
```
UART
```
```
UART
```
```
USB
```
```
CAN
```
```
CAN
```
```
CAN
```
```
Arm camera
USB
Gripper’s stepper motorGPIO/UART
```
```
Load sensor x
```
```
I2C/SPI
```
```
Ethernet
CAN
```
```
USB Nav Camera x
```
```
MIPI CSI-2 Main Nav Camera
```
```
USB Wi-Fi Adapter (mast)
```
```
UART Fallback antenna
```
```
USB Spectral camera
```
```
GPIO / PWM
```
```
USB USB <- CVBSAdapter PAL CVBS Thermal camera
```
```
microcontrollerContainer
CAN
```
```
Lid motor x
PWM
```
```
I2C Drill Motor+ Driver
```
```
Weight amplifier x3Tensor sensor +
GPIO
I2C IMU
```
```
microcontrollerAstrobio ADC pH Sensor
```
```
Liquid Pump+ Driver
```
```
PWM
```
```
Liquid Level Sensor
```
```
GPIO
```
```
UART
```
```
Activity Indicator
GPIO
```
```
Legend
Unidirectional data flow
Bidirectional data flow
Subsystem boundary
Figure 1: Control system architecture
```
### 3.2 Rover Design Description

#### 3.2.1 Mechanical Design

##### 3.2.1.1 Chassis Configuration and Geometry

The chassis is the rover structural platform integrating all major subsystems in a four-wheel rocker-bogie
layout built from aluminium profiles. An external differential link couples the rocker arms and balances
left-right terrain loads for stability. Preliminary dimensions are approximately 1_._ 2 m× 0_._ 8 m× 0_._ 7 m(L
×W×H), subject to refinement during detailed design. All four wheels are driven and steered, each
with a full 360°steering range (Figure 2).

```
Figure 2: Assembled rover system with labeled subsystems
```

##### 3.2.1.2 Drive Calculation and Selection

```
Drive sizing is based on two governing load cases: traction on a 15 ◦slope and step climbing. Here, Crr is the
coefficient of rolling resistance (dimensionless). The traction model uses rolling resistance F roll= Crrmg ,
grade force F grade= mg sin α , acceleration force F acc= ma , and total force F tot= F roll+ F grade+ F acc.
The step model uses W lead= mg/N as the load on the wheel that first contacts the obstacle.
The step-climbing model applies to the wheel that first contacts the obstacle. Therefore, it is valid for
both forward and reverse motion (front-leading or rear-leading axle). In this preliminary model, forward
and reverse limits are assumed identical: v = 1 m s−^1 and a = 1 m s−^2. Details in Table 3.
```
- **Traction case (** 15 ◦ **slope):** _τ_ wheel≈ 12_._ 7 N mper wheel.
- **Rated requirement:** _τ_ rated= _τ_ wheel _ks/η_ ≈ 23_._ 8 N mfor _ks_ = 1_._ 5 , _η_ = 0_._ 8.
- **Step-climbing case:** for _r_ = 0_._ 15 m, nominal limit40 N mgives _h_ ∗≈ 0_._ 127 m (≈ 0_._ 85 _r_ ).
- **Motor selection:** chosen drive motor provides40 N mnominal and120 N mpeak at 48 V.

```
Table 3: Drive motor torque requirements ( r = 0. 15 m, m = 75 kg, N =4wheels)
```
```
Load case Expression Value Note
Traction model
Rolling resistance F roll= Crrmg 73. 6 N Crr = 0. 10
Grade force F grade= mg sin α 190. 4 N α = 15◦
Acceleration force F acc= ma 75. 0 N a = 1 m s−^2
Total traction force F tot= F acc+ F roll+ F grade 339. 0 N
Wheel torque τ wheel= F tot r/N 12. 7 N m per wheel
Rated requirement τ rated= τ wheel ks/η 23. 8 N m ks =1. 5 , η =0. 8
Step-climbing model
Leading wheel load W lead= mg/N 183. 9 N equal static wheel load
```
```
Step torque τ step( h ) = W lead r
```
###### √

```
2 rh − h^2
r − h
```
###### —

```
Max obstacle (nominal) τ step( h ∗) = 40 N m h ∗≈ 0. 127 m 0. 85 r
Max obstacle (peak) τ step( h ∗∗) = 120 N m h ∗∗≈ 0. 148 m 0. 99 r
```
##### 3.2.1.3 Wheel Design

```
The rover wheels are single-piece thermoplastic polyurethane (TPU) components, selected to reduce
assembly complexity and provide controlled compliance on irregular terrain. A straight-line tread pattern
is used to improve longitudinal traction and reduce lateral slip on loose soil and mixed rocky surfaces
typical of the ERC Mars Yard.
To reduce unsprung mass, the wheel body uses a perforated web pattern. The current wheel revision is
the baseline for mass, traction, and endurance testing, with a design target of limiting peak deformation
to5 mmunder the expected wheel load envelope.
```
##### 3.2.1.4 Manipulator Configuration and Kinematics

The 6-DOF articulated manipulator is designed for a maximum payload of 3 kgand provides a maximum
reach of 132 cm. It features an open serial kinematic chain with an anthropomorphic RRR (Revolute-
Revolute-Revolute) positioning structure and a spherical wrist. The configuration is shown in Figure 3.
The system is divided into two decoupled functional groups to simplify Inverse Kinematics (IK) compu-
tation. The positioning subsystem ( _q_ 1 : base rotation, _q_ 2 : shoulder pitch, _q_ 3 : elbow pitch) dictates the
( _x,y,z_ )coordinates of the wrist center. The orientation subsystem utilizes a spherical wrist ( _q_ 4 – _q_ 6 : wrist
pitch, roll, yaw) with axes intersecting at a single point, controlling the end-effector’s approach angle
independently of its spatial position. This architecture ensures a versatile workspace envelope (detailed
in the reachability drawings) that effectively accesses both ground-level targets for sample collection and
elevated panels for maintenance tasks.

##### 3.2.1.5 Load Analysis and Selection of Manipulator Actuators

```
The torque requirements in the joints are determined based on a vector dynamic model of the manipulator,
which takes into account gravitational, inertial, frictional and external loads:
```
```
Mmotor = Mgravity + Mfriction + Minertia = mgr ⊥+ Mfr + Jβ,
```
```
where m is the equivalent mass acting on the joint (kg), g is the gravitational acceleration (m s−^2 ), r ⊥is
the perpendicular distance from the joint axis to the line of action of the weight (m), Mfr is the friction
```

```
(a) Deep sampling (b) Bioscience
```
```
(c) Probe gathering (d) Maintenance
Figure 3: Manipulator configuration and operational scenarios
```
torque (N m), _J_ is the equivalent moment of inertia referred to the joint axis (kgm^2 ), and _β_ is the angular
acceleration of the joint (rad s−^2 ).
The positioning subsystem ( _q_ 1 – _q_ 3 ) utilizes direct-drive high-torque planetary actuators, while the orienta-
tion subsystem ( _q_ 4 – _q_ 6 ) is driven by low-torque planetary actuators (peak horizontal loads in Table 4).

```
Table 4: Calculated peak joint loads with estimated uncertainty and selected actuator torques
```
```
Joint (Coordinate)
Calculated Peak
Load [ N m ]
```
```
Motor Rated
Torque [ N m ]
```
```
Safety
Factor
q 1 ,q 2 (Base, Shoulder) 44. 9 ± 4. 0 48 1.
q 3 (Elbow) 16. 2 ± 1. 5 48 2.
q 4 ,q 5 ,q 6 (Wrist) 2. 84 ± 0. 30 9 3.
```
All motion units are equipped with position encoders for closed-loop feedback: the wrist actuators use
dual 14-bit single-turn magnetic encoders, while the high-torque arm actuators are equipped with dual
14-bit magnetic encoders.

##### 3.2.1.6 End-Effector Design

The manipulator uses a standardized quick-change interface with integrated electrical coupling for rapid,
tool-less swapping between three end-effectors: a parallel-jaw gripper, a sample end-effector, and an
astrobio end-effector. The interface is tolerant to minor misalignment and provides reliable mechanical
and electrical connection. An overview of the available tools is shown in Figure 4.
**Parallel-Jaw Gripper**
For maintenance operations and solid sample collection, the gripper (Figure 4a) provides a maximum
jaw opening of 105 mmwith parallel finger motion across the full stroke. Gripping faces are 30 × 32 mm
with compliant rubber pads, and fingertips taper to 10 mm. Maximum open-envelope dimensions are
180 × 200 × 80 mm(W×L×H). A stepper motor with step-skipping overload protection drives the
mechanism, while load sensors provide closed-loop force control. The quick-change interface supports
button pressing, knob rotation, switch toggling, and probe handling up to30 mmdiameter.
**Sample End-Effector**
This tool (Figure 4b) replaces the gripper fingers with opposing bucket scoops while retaining the
dual-linkage mechanism. The buckets provide 700 cm^3 total volume and collect at least200 gof regolith
per pass. Rubber-lined rims and full wrist articulation allow secure handling of rocks up to 15 cm. A
shoulder-driven, perpendicular Archimedean auger ( 335 mmlength, 35 mmdiameter) enables penetration
beyond30 cmwhile minimizing distal mass.


```
(a) Parallel-Jaw Gripper (b) Sample End-Effector (c) Astrobio End-Effector
Figure 4: Manipulator end-effectors used for maintenance and sampling tasks
```
**Astrobio End-Effector**
The astrobio tool (Figure 4c) uses a sealed 300 mLcontainer with a distal pump and dual tubes (air
evacuation and liquid intake). Integrated pH and liquid-level sensing, plus a local microcontroller, provide
autonomous sampling and telemetry to the main system. A spring-loaded telescopic intake verifies full
submersion before pump start, and the level sensor stops filling automatically. A sealed service port
enables pH probe recalibration without disassembly.

##### 3.2.1.7 Sample Storage and Weighing System

The outer container ( 503 × 180 × 120 mm), mounted on the rover front chassis, houses three inner cups:
regolith ( 160 × 160 × 100 mm), rock ( 160 × 160 × 100 mm), and deep sample ( 80 × 160 × 100 mm); the deep
cup accommodates the35 mmauger diameter, while rock specimens up to15 cmfit, as natural samples
rarely exceed 10 cmin other axes. A two-part servo-driven lid autonomously opens on a container-ready
signal, accepts the deposit, then closes and locks. Each cup is mounted on an independent load cell
channel sampled simultaneously by the container microcontroller; under rover tilt, the measured force
follows _F_ = _mg_ cos _θx_ cos _θy_ , with true mass recovered as _m_ = _g_ cos _θFx_ cos _θy_ , compensating with IMU data

for uneven terrain. Corrected values are transmitted via CAN to the main computer, achieving±1 g
resolution independent of rover orientation.

```
Figure 5: Sample storage container: 3D model (left) and engineering drawing (right)
```
#### 3.2.2 Electrical Power Subsystem

##### 3.2.2.1 Battery Configuration and Hot-Swap Design

The battery subsystem uses hot-swappable commercial lithium-ion e-bike/scooter modules (each48 V,
12 A h) in a 3 to 4 -module parallel configuration, giving36 A hto48 A hbased on mission demand;
modules are mounted on a rail hot-swap dock for fast tool-free replacement, include integrated BMS
protection, and improve resilience through current sharing, with dynamic-load validation planned and an
external protection/balancing stage added only if required (see § 3.1.3).

##### 3.2.2.2 Power Distribution and Regulation

The rover’s power system is centered around a 48V DC bus supplying all onboard consumers.
**Safety and Control Segment (Always-on):** Powered directly from the 48V bus before the main
contactor, this segment uses regulated 24V, 5V, and 3.3V rails via DC-DC converters to support the
emergency stop system, control logic, and communications, ensuring operation even when the main power
is disconnected.


A A

B B

C C

D D

```
1
```
```
1
```
```
2
```
```
2
```
```
3
```
```
3
```
```
4
```
```
4
```
```
5
```
```
5
```
```
TITLE: Sheet_2 REV:1.
```
```
Date: 2026-04-
```
```
Sheet:1/
Drawn By:yarynaaaaaa
```
```
Company:Your Company
```
```
Battery 1
```
```
Battery 2
```
```
BMS
```
```
BMS
```
```
Buck
```
```
Buck Converter5V
```
```
Buck Converter3.3V
```
```
Buck Converter
24V
```
```
Consumers
```
```
e-stop E-stop Controller
```
```
48V
```
```
48V
```
```
Battery 3 BMS Converter
24V
```
```
Converter3.3V
Buck
```
```
Remote
```
```
switch ON/OF EStop-Button Remote
```
```
switch ON/OF
```
```
EStop-Button
```
```
transciever
Safety and Control Segment
```
```
Sensors and
communication
interfaces
```
```
Computing
units
```
```
Motor drivers
hardware
```
```
and auxiliary
```
```
Traction motors
and high-power
actuators
```
```
Figure 6: Power distribution and consumers schematic diagram
```
```
Main Power Segment: Activated via the main contactor, this segment distributes power to all
operational consumers, with 48V, 24V, 5V, and 3.3V rails provided through DC-DC converters.
The Emergency Stop system is described in § 3.4.1.
```
#### 3.2.3 Communication Subsystem

##### 3.2.3.1 Communication Architecture Overview

- All operator equipment is deployed inside the team zone within a dedicated ground-station unit.
- Rover communication uses one primary Wi-Fi low-band channel at 5 GHz(video, telemetry, and
    commands), with a fallback transceiver at 430 MHzto 440 MHzand a separate e-stop link at
    430 MHzto440 MHz.
- The antenna mast hosts the mast computer, Wi-Fi adapter, Fallback link, separate e-stop link,
    directional Wi-Fi antenna, and is connected to the ground station unit (Figure 7).

```
ROVER ANTENNA MAST
```
```
DRONE
```
```
GROUND STATION
```
```
Drone Reception
```
```
E-Stop MCU | ESP
E-Stop TRX | 433 MHz
Fallback TRX | 433 MHz
Wi-Fi Adapter | 5 GHz
```
```
Main ComputerJetson
Cameras
Rover Control
Telemetry
```
```
Mast ComputerRaspberry
E-Stop TRX | LoRa 433 MHz
Fallback TRX | LoRa 433 MHz
Wi-Fi Adapter | 5 GHz
```
```
FPV Camera
FPV TX | 5.8 GHz
RC Receiver | 2.4 GHz
Telemetry (air) | 433 MHz
```
```
Ground Station PCUI | video | rosbridge client
```
```
Monitors | Rover Controller
```
```
FPV RX 1 — Pilot | 5.8 GHz
FPV Goggles
FPV RX 2 — GS | 5.8 GHz
Capture Card
RC Controller | 2.4 GHz
Telemetry (GS) | 433 MHz
```
```
video
```
```
tlm
```
```
5 GHzWi-Fi
PRIMARY
```
```
ETH + PoE
```
```
433 MHz | Fallback
```
```
433 MHz | E-Stop
```
```
5.8 GHz
```
```
5.8 GHz
```
```
2.4 GHz
433 MHz
```
```
LINKS: Wi-Fi / ETH – – – 433 MHz Fallback – – – 433 MHz E-Stop - - - - - Drone RF Internal lines
MODULES: Rover Antenna Mast Ground Station Drone FPV / Drone RF Redundancy / Safety Main Computer
```
```
Figure 7: Ground station communication architecture.
```
```
Detailed frequency allocation, redundancy, and link performance are covered in § 3.2.3.2 through § 3.2.3.5.
```
##### 3.2.3.2 Frequency Plan

```
Rover RF allocation is listed in Table 5.
```

```
# Link Band Hardware
1 Primary rover Wi-Fi 5150 MHzto5725 MHz Wi-Fi Adapter× 2
2 Rover fallback 430 MHzto440 MHz Fallback Transceiver× 2
3 E-Stop 430 MHzto440 MHz E-Stop Transceiver× 2
Table 5: RF link allocation. Full parameters in RF Form (Appendix 5).
```
##### 3.2.3.3 Link Performance Analysis

```
TX power and antenna gain are taken from hardware datasheets, RX sensitivity from IEEE 802.11ac, and
the resulting budget is summarized in Table 6. Free-space path loss is calculated via the Friis equation:
```
```
FSPL [dB] = 20 log 10 ( d ) + 20 log 10 ( f )− 147. 55 (1)
```
```
where d is distance in metres and f is frequency in Hz.
Table 6: Wi-Fi link budget at100 m, 5. 24 GHz
Parameter Line-of-Sight Non-Line-of-Sight
TX power (Wi-Fi Adapter) 20 dBm 20 dBm
TX antenna gain (Directional Antenna) +10 dBi +10 dBi
TX cable loss -0.5 dB -0.5 dB
EIRP 29.5 dBm 29.5 dBm
FSPL @100 m -86.8 dB -86.8 dB
Terrain obstruction loss 0 dB -20 dB
RX antenna gain (rover dipole) +2 dBi +2 dBi
Received power -55.3 dBm -75.3 dBm
RX sensitivity (MCS7 / MCS0) -68 dBm -82 dBm
Link margin +12.7 dB +6.7 dB
```
##### 3.2.3.4 Bandwidth Management

Bandwidth is managed through H.265 video compression on the Main Computer, with per-task profiles
enabling only required camera streams, and through Rosbridge throttling that downscales high-rate topics
(IMU, odometry) while sending low-rate topics (arm joints, science sensors) only on change.

##### 3.2.3.5 Communication Redundancy

- **Fallback Transceiver** - dedicated LoRa channel at 430 MHzto 440 MHzon; preserves command
    and essential telemetry at reduced throughput if Wi-Fi fails
- **E-Stop link** - separate dedicated LoRa 430 MHzto 440 MHzchannel, independent of all the other
    systems

#### 3.2.4 On-Board Sensor and Imaging Systems

##### 3.2.4.1 Navigation Sensor Suite

```
The navigation sensor suite provides near- 360 ◦perception for simultaneous state estimation and collision
avoidance.
```
- **Front stereo vision sensor (ZED 2i):** Mounted at the front of the rover, it provides RGB
    imagery and depth data at a resolution of 1280 × 720 , a frame rate of 60 fps, a field of view of
110 ◦× 70 ◦(H×V) and an effective depth range of 0_._ 3 mto20 m, includes an integrated 6-axis IMU
(400 Hz).
- **Top LiDAR (RPLIDAR S2):** Mounted at the top of the rover, it provides 360 ◦2D scanning
    with 0_._ 12 ◦angular resolution at 10 Hz, ensures reliable obstacle detection up to10 macross varying
    lighting and reflectivity conditions.
- **Side and rear close-range coverage sensors (3** × **Maix Sense A010 ToF):** Mounted on the
    mast in the center of the rover, these sensors face left, right, and rear to serve as an additional
    measure for close obstacle detection, providing 210 ◦of non-forward coverage. Each sensor outputs
    a 100 × 100 depth map at up to 20 fpswith a 70 ◦× 60 ◦(H×V) FoV and an effective range of 0_._ 2 m
    to 2_._ 5 m.
- **Wheel odometry:** Odometry is provided by 14-bit single-turn absolute magnetic encoders on all
    8 motors used for the swerve drive.
The stereo camera (specifically utilizing its depth and IMU data), LiDAR, and encoders provide input
to state estimation and localization (§ 3.2.5.1), while all vision and ranging sensors support collision
avoidance (§ 3.2.5.2). The RGB imagery from the ZED 2i is further utilized for teleoperation (§ 3.2.4.3).


##### 3.2.4.2 Science Sensor Suite

The pH sensor is calibrated via three-point protocol at buffer solutions prior to each mission run,
establishing a voltage-to-pH gradient with measurement of± 0_._ 1 pH. Repeatable performance is validated
through consecutive measurements of a reference solution within the± 0_._ 1 pHtolerance — demonstrating
sensor stability under field conditions sufficient for planetary astro-biological liquid analysis.

##### 3.2.4.3 Rover Camera Suite

The primary camera suite supports navigation, situational awareness, and arm operations:

- **Front Stereo Camera:** Detailed specifications are provided in § 3.2.4.1.
- **Main Nav Camera:** Mast-mounted elevated forward view for terrain, deck, and arm monitoring;
    2560 × 720 at93 fps, with 120 ◦left and 90 ◦right field of view.
- **Nav Cameras:** Front and rear cameras; 1920 × 1200 at50 fps, 150 ◦diagonal field of view.
- **Arm Camera:** Mounted above the gripper for manipulation and close-range detection; 1920 × 1200
- **Illumination:** Two front wide-angle lamps and one arm-camera ring lamp provide low-light support
    for navigation and manipulation; activation is automatic via a light-level sensor.
- **Multispectral Camera:** Mounted on the front-left corner of the rover chassis; imaging at 490 nm,
    615 nm, and 808 nm, selected for the Dao/Niger Vallis zone. It targets Fe-rich pyroclastics (unit HNhf;
    volcanic ash) overlying basaltic plains (unit HNpr; bedrock). It utilizes IAEI (Iron Absorption Edge
    Index; Fe-mapping) and HGI (Hematite–Goethite Index; water indicator) to delineate lithological
    boundaries and discriminate past aqueous activity consistent with Leonard & Tanaka (2001).
- **Thermal Camera:** Mounted on the front-right corner of the rover chassis; for surface anomaly
    detection. Combined with IAEI (iron-index) maps, it uses thermal contrast to correlate thermal
    inertia, discriminating loose pyroclastic material from dense basalt.

#### 3.2.5 Software Architecture

The software stack is built on ROS 2 Humble as the middleware framework, providing standardized
inter-process communication via topics, services, and actions, as well as integration with the broader ROS
2 ecosystem of navigation, perception, and control packages described in the following sections.

##### 3.2.5.1 State Estimation and Localization

Based on competition rules, we defined the localization requirement as an absolute pose error below 0.
m over a 150 m route. To satisfy this in variable lighting and feature-poor environments, we implemented
the dual-layered pipeline illustrated in Figure 8.
The local Extended Kalman Filter (EKF) fuses visual-inertial and wheel data for smooth, high-frequency
odometry. Global Simultaneous Localization and Mapping (SLAM) corrects drift via scan matching,
anchoring the rover to the map without inducing local state jumps.
The system achieves absolute positioning by detecting ArUco markers at known coordinates. Inverting the
marker’s 6D pose relative tobase_linkand projecting it to the ground plane, the pipeline calculates a
zero-drift global pose. This update is injected into the global layer to correct the map transform, ensuring
precise navigation toward featureless waypoints.

```
Wheel Encoders
```
```
Stereo Camera
+ IMU
```
```
LiDAR
```
```
Encoder Bridge
encoder_bridge
```
```
ZED Wrapper
zed_node
```
```
LiDAR Driver
s2_lidar_node
```
```
Swerve Kinematics
swerve_node
```
```
ArUco Detector
aruco_node
```
```
Local EKF
ekf_filter_node
```
```
SLAM
slam_toolbox
```
```
Nav2 Stack
```
```
HARDWARE Drivers Perception & Kinematics State Estimation
```
```
SOFTWARE
```
```
Encoder Ticks
```
```
Stereo Image& IMU data
```
```
Laser Scan
```
```
/joint_states
```
```
/zed/odom
```
```
/zed/image_raw
```
```
/scan
```
```
/wheel_odom
```
```
/aruco/pose
```
```
( odom →/tf base _ link )
```
```
/odom&/tf
( odom → base _ link )
```
```
( map /tf→ odom )
```
```
Figure 8: Perception and localization pipeline architecture.
```
##### 3.2.5.2 Autonomous Navigation and Collision Avoidance

The navigation subsystem is implemented using the Nav2 framework with custom costmap plugins. Data
flow from sensors to velocity commands is shown in Figure 9.

- **Global planning:** nav2_navfn_planner(Dijkstra) on a 0_._ 05 mresolution 2D global costmap.


```
HARDWARE COSTMAP
```
```
NAVIGATION & LLOCALIZATION
```
```
Stereo Camera
```
```
ToF Cameras
```
```
LiDAR
```
```
Voxel Layer
```
```
Obstacle Layer
```
```
Inflation Layer
```
```
State Estimation
EKF + SLAM / TF tree
```
```
Global Planner
NavFn / Dijkstra
```
```
Local Controller
DWB
```
```
Motor Controllers
```
```
/stereo/points
```
```
/tof_camera/points
```
```
/scan
```
```
Occupancy Grid
```
```
Aggregated Grid
```
```
/global_costmap/costmap
```
```
/local_costmap/costmap
```
```
/tf
```
```
/odom&/tf
```
```
/plan
```
```
/cmd_vel
```
```
Figure 9: Costmap and motion planning pipeline architecture.
```
```
IDLE
waiting for goal
```
```
GOAL REACHED
goal condition
```
```
PLAN PATH
global planner
```
```
FAIL-SAFE STOP
no safe path
```
```
TRACK PATH
local control
```
```
LOCAL RECOVERY
obstacle avoidance
```
```
goal received path found
```
```
local path clear
```
```
goal reached: within predefined threshold and rover stopped
```
```
await next goal global path invalid local path blocked
```
```
global path invalid
```
```
planning failed
```
```
reset / operator
Figure 10: Navigation state machine: goal tracking, recovery, and fail-safe behavior
```
```
Replanning triggered on path invalidation.
```
- **Local control:** nav2_dwb_controllergenerating holonomic( _vx,vy,ω_ )commands for swerve-drive
    kinematics with real-time obstacle response.
- **Collision avoidance:** nav2_costmap_2dwith voxel, obstacle, and inflation layers. 3D perception
    projected to 2D costmaps; safety margin enforced via inflation radius.
- **Task execution:** nav2_bt_navigatororchestrating navigation via behavior trees; recovery and
    fail-safe actions implemented withnav2_behaviors.

The costmap integrates stereo, ToF cameras, and LiDAR data (§ 3.2.4.1). 3D terrain geometry (slope
and surface variation) is projected onto the 2D costmap for traversability estimation.
Recovery behaviors, including replanning and fail-safe stop transitions, are illustrated in Figure 10.

##### 3.2.5.3 Arm Kinematics and Motion Planning

The software stack is divided into four modules. The modeling module uses Unified Robot Description
Format (URDF) / XML Macros (Xacro) to define links, joints, limits, inertial parameters, and collision ge-
ometry, while the MoveIt 2 configuration package stores Semantic Robot Description Format (SRDF) data,
planning groups, and semantic collision settings. The main packages here arerobot_state_publisher,
MoveIt Setup Assistant, and the generated MoveIt config package. The kinematics and planning mod-
ule is centered aroundmove_group; inverse kinematics is handled bykdl_kinematics_plugin(KDL,
Kinematics and Dynamics Library), while Open Motion Planning Library (OMPL) is used for collision-
free path generation and MoveIt planning adapters are used for trajectory post-processing and time
parameterization.
The execution module is implemented throughros2_control(ROS 2), wherecontroller_manager
manages the hardware interfaces and controller lifecycle,joint_trajectory_controllerexecutes joint-
space trajectories, andjoint_state_broadcasterpublishes the current joint states. The perception
integration module uses custom ROS 2 nodes together with Transform Library 2 (TF2) to transform
Computer Vision (CV) targets from the arm camera frame into the manipulator base frame and to update
the MoveIt planning scene with collision objects and obstacles. Details in Figure 11.

##### 3.2.5.4 Science Autonomous Operation Architecture

Three fully autonomous sampling pipelines are implemented (Figure 12); each executes without operator
input from initial detection through sample deposit and mass confirmation.


```
URDF/Xacro
robot model
```
```
MoveIt 2 config
SRDF, limits, groups
```
```
move_group
motion planning
```
```
kdl_kinematics_plugin
inverse kinematics
```
```
OMPL
path planning
Planning adapters
time parameterization
```
```
CV module
target detection
TF2 + custom ROS 2 nodes
arm camera→base transform
```
```
Planning scene
obstacles / collision objects
```
```
ros2_control
controller_manager
```
```
joint_trajectory_controller
trajectory execution
Figure 11: Manipulator motion planning and execution pipeline.
Photo pre-drill
Drill 300 mm
Retract drill
Photo post-drill
Position arm with drill above container
Open container
Reverse drill rotate — deposit collected materials
```
```
Check collected weight
m ≥ 100 g
```
```
Close container
Park arm
Log mass
```
```
yes
```
```
no
```
```
Detect sample/rock
Grasp sample
Lift arm above container
Open container
Release sample from arm gripper
```
```
Check collected weight
m ≥ 100 g
```
```
Close container
Park arm
Log mass
```
```
yes
```
```
no
```
```
Detect cup
Insert tube
```
```
Check if tube in liquid
```
```
Pumping
```
```
Check amount of liquid
V ≥ 100 ml
```
```
Stop pumping
Measure pH
Log pH
Park arm
```
```
yes
```
```
no
```
```
yes
```
```
no
```
```
(a)
```
```
(b)
```
```
(c)
Figure 12: Autonomous science sampling pipelines: (a) Deep sampling pipeline; (b) Surface/stone
sampling pipeline; (c) Liquid sampling pipeline.
```
#### 3.2.6 Operations

##### 3.2.6.1 Ground Station Setup and Equipment

```
The Ground Station Unit provides operators with real-time control, data visualization, and status
monitoring. Its core setup includes:
```
- **Ground Station PC:** Handles video decoding and telemetry monitoring.
- **User Interface:** Features two monitors, a control panel with buttons and switches, and a **Rover**
    **Controller** for manual navigation.
- **Directional Antenna:** A tripod-mounted, adjustable antenna for optimal rover communication.
    It connects to the station via an Ethernet cable and is positioned within a20 mradius.

##### 3.2.6.2 Teleoperation and Control Interface

```
The teleoperation framework supports three control modes: the Ground Station Unit(GSU) provides
manual rover and subsystem control, the drone uses a separate remote controller independent of the
GSU , and autonomous lockout limits feedback to telemetry only by disabling camera imagery.
```
### 3.3 Rover Technical Budgets

#### 3.3.1 Mass Budget and Per-Task Configuration Breakdown

```
Calculation basis ( Table 7, Table 8, Table 9 ): base rover configuration 35.7 kg, electronics 13.3 kg,
manipulator arm 8.8 kg, exploration cameras 0.16 kg, sample end-effector 1.54 kg, container system 1.
kg, astrobio end-effector 0.7 kg, landing platform 0.8 kg (preliminary estimate).
```
#### 3.3.2 CoG Analysis and Slope Stability

CoG height is estimated with a two-group mass model: mobile platform + electronics ( 49_._ 0 kg at 270
mm) and manipulator arm ( 8_._ 8 kg at 620 mm), giving _h_ =^49_._^0 ·270+8 57_._ 8_._^8 ·^620 ≈ 323 mm_._ Static tipping angle
is _α_ tip=arctan( _d/h_ ): 48_._ 1 ◦for lateral loading ( _d_ = 360mm, critical) and 61_._ 7 ◦for longitudinal loading
( _d_ = 600mm).


```
Table 7: Rover mass budget – mobile platform and electronics (preliminary estimate)
Mobile Platform (Suspension)
Component Qty Mass (kg)
Frame profiles and furniture — 5.
Body panels and box assembly— 8.
Rocker arms 2 2.
Central axis 1 1.
Hub frame and wheel disc 4 6.
Tyres, TPU 4 2.
Drive motor 4 5.
Wheel steering motor 4 1.
Total (mobile platform) 31.
```
```
Electronics and Power
Component Qty Mass
(kg)
Main compute module 1 1.
Stereo camera 1 0.
ToF camera 3 0.
LiDAR 1 0.
Battery packs 4 12.
Harness, cables, and buck
converters
```
```
1 set 1.
```
```
Total (electronics) 13.
```
Table 8: Rover mass budget – manipulator arm and science station (preliminary estimate)
**Manipulator Arm
Component Qty Mass (kg)**

Joint motors 6 4.
Carbon-fiber tubes set 1 (1 m set) 1.
Depth camera class 1 0.
Wiring and cables 1 set 0.
Gripper 1 0.
3D-printed mounts and joint
parts

```
1 set 1.
```
**Total (arm subsystem) 8.**

```
Science Station
Component Mass
(kg)
Sample end-effector 1.
Container system 1.
Astrobio end-effector (with analyzers) 0.
Exploration cameras 0.
Total (science station) 4
```
```
Table 9: Per-task rover configuration mass summary
Task Arm Task payload/tool Formula (kg) Total (kg)
Navigation task No None 35. 7 + 13. 3 49.
Maintenance task Yes None 35. 7 + 13. 3 + 8. 8 57.
Exploration task No Exploration cameras 35. 7 + 13. 3 + 0. 16 49.
Deep sampling
task
```
```
Yes Sample end-effector
+ container system
```
###### 35. 7 + 13. 3 + 8. 8 + 1. 54 + 1. 6 60.

```
Astrobiology task Yes Astrobio end-effector 35. 7 + 13. 3 + 8. 8 + 0. 7 58.
Droning task No Rover-mounted
landing platform
```
###### 35. 7 + 13. 3 + 0. 8 49.

#### 3.3.3 Power Budget

**Operating modes used in budget.** Two modes are evaluated: _Locomotion_ (drive, steering, baseline
electronics) and _Manipulator_ (arm operation with interchangeable end-effectors: gripper, auger bucket,
liquid-sampling module).
**Mode 1: Locomotion (Table 10).** Drive power is estimated from traction: _P_ loc= _P_ drive+ _P_ steer _,_ avg+
_P_ base_._

```
F trac= mg (sin θ + μr cos θ ) , T wheel=
```
```
F trac rw
4
```
```
, I drive≈ 4 I nom
```
```
T wheel
T nom
```
```
, P drive= UI drive.
```
Assumptions from Table 3: _rw_ = 0_._ 15 m, _m_ = 75kg, _θ_ = 15◦, with motor electrical parameters _U_ = 48 V,
_T_ nom= 40 N m, _I_ nom= 23_._ 5 A.
**Mode 2: Manipulator (Table 11).** Manipulator-mode power is evaluated as base arm load plus
end-effector increment. All values are preliminary (±15 %, pending bench validation). For 3 to 4 battery
modules,
_E_ bat= 1728 W hto2304 W h _, E_ loc _,_ 60 ≈1366 W hto1817 W h_._

For the mixed60 minprofile ( _t_ loc= 30 min, _t_ grip= _t_ auger= _t_ liquid= 10 min),

```
E tot= 0. 5 h P loc+ 0. 1667 h
```
###### (

```
P grip+ P auger+ P liquid
```
###### )

###### .


```
Table 10: Locomotion power budget (preliminary)
Term Expression / basis Value
```
```
Drive power P drive
μr = 0. 10 (compact)
μr = 0. 25 (softer terrain)
```
###### 1106 W

###### 1557 W

```
Steering average P steer , avg
P steer , peak D, P steer , peak= 1636 W
D = 0. 05 to 0. 15
```
```
81. 8 Wto 245. 4 W
nominal164 W
Baseline P base conservative constant 96 W
Total locomotion P loc P drive+ P steer , avg , nom+ P base 1366 Wto1817 W
Locomotion energy for60 min, E loc P loc·1 h 1366 W hto1817 W h
```
```
Table 11: Manipulator power budget (preliminary)
Configuration / term Expression Power
Joint actuator group P joint 3 ·48 V· 8. 53 A 1228 W
Wrist actuator group P wrist 3 ·48 V· 2. 5 A 360 W
Base actuator power P arm , motors , base P joint+ P wrist 1588 W
Auxiliary electronics P aux constant 20 W
Base manipulator power P arm , base P arm , motors , base+ P aux 1608 W
Gripper attachment ∆ P tool= 18 Wto36 W P arm , total= 1626 Wto1644 W
Auger bucket attachment ∆ P tool= 35 Wnominal (247 W
short peak)
```
```
P arm , total= 1643 Wnominal
```
```
Liquid-sampling attachment ∆ P liquid≈20 W(preliminary) P arm , total≈1628 W
```
```
Using nominal values, E tot≈1620 W h. The liquid-sampling load does not change the battery-count
conclusion: 3 modules provide limited margin, while 4 modules provide comfortable margin. These
estimates indicate that the rover can sustain the required 60 minmission duration under the considered
operating profile.
```
#### 3.3.4 Data Link Budget

```
H.265 bitrate targets are set on the Main computer using NVENC. NVENC is separate from CPU/GPU
cores, so encoding load is low. We assume a conservative usable link capacity of 40 Mbits−^1 (about 20%
of the200 Mbit s−^1 802.11ac40 MHzpeak) to account for overhead, retries, and interference.
Per-stream H.265 bitrate estimates:
```
- Video feed:17 Mbit s−^1
- Telemetry + commands: _<_ 1 Mbit s−^1

Worst-case total is about 18 Mbits−^1 , leaving about 22 Mbits−^1 headroom (∼55%of estimated capacity).

### 3.4 Rover Safety Systems

#### 3.4.1 Emergency Stop System

```
The emergency-stop architecture uses multiple independent interruption points to provide immediate
rover power isolation:
```
- **Physical E-stop:** a local emergency button directly interrupts the main contactor coil.
- **Remote E-stop (GS):** a clearly marked ground-station button sends a stop command via a
    dedicated e-stop transceiver link (GS to rover).
- **Controller cutoff logic:** the onboard E-stop controller processes local/remote stop signals and
    opens the power path through the contactor control relay, including remote OFF/failsafe signal-loss
    behavior.
The contactor control and E-stop implementation is shown in Figure 6.

#### 3.4.2 Motion Warning and Delay System

```
An industrial lamp mounted at the rover’s highest point ensures 360 ◦visibility. It uses high-intensity
blinking LEDs visible from10 min direct sunlight. The lamp uses four colors to indicate the rover’s state:
orange (powered on), green (manual control), red (autonomous mode), and blue (wireless connection to
the ground station).
A mandatory5 ssoftware delay precedes all rover and subcomponent movements. Upon command, the
lamp activates immediately while the rover holds a safe, completely still standby mode. Command
broadcasts are blocked during this window to prevent premature execution. Movement begins post-delay,
with the signal remaining active until operations finish.
```

```
Table 12: Radio frequency (RF) link allocation. Full parameters in RF Form (Appendix 5).
# Link Band Hardware
1 RC Link 2. 4 GHz RC Transmitter & Receiver
2 Video Link 5725 MHzto5875 MHz Video Transmitter & Receiver
3 Telemetry Link 433 MHz Telemetry Transceivers
```
#### 3.4.3 Human Detection Safety System

The system utilizes four human presence sensors to provide overlapping 360 ◦coverage. Each sensor
features a 120 ◦FoV and tracks a maximum of three individuals at a range of up to6 m.
The onboard software calculates the relative position of all detected targets in real time, continuously
streaming this data to the ground station. Proximity alerts trigger at4 m, appearing directly on the
ground station’s control interface. To ensure personnel safety, the system executes an automatic emergency
stop if an individual enters the critical zone:2 mat the front or1 mat the sides and rear.

### 3.5 Drone Design Description

#### 3.5.1 Physical Design and Environmental Resilience

##### 3.5.1.1 Drone Overview

The Drone is a quadcopter built from Commercial Off-The-Shelf (COTS) components. Figure 13 provides
a high-level view of its onboard electronics architecture and subsystem interfaces.

```
Navigation Subsystem Communication Segment
```
```
Core Avionics Subsystem Perception & Video Subsystem
```
```
Propulsion Subsystem
```
```
Flight Controller
```
```
Companion
Computer
```
```
UART
```
```
GPS & Compass UART & I2C
```
```
Optical Flow Sensor UART
```
```
RC Receiver
```
```
Telemetry Radio
```
```
RC Controller
```
```
Ground Station
```
```
2.4 GHz RF
```
```
433 MHz RF
```
```
UART
```
```
UART
```
```
Downward CV Camera
```
```
Forward Camera
Video Switcher Video Transmitter(VTX)
```
```
MIPI CSI-
CVBS
CVBS
```
```
CVBS
```
```
5.8 GHz RF
```
```
Electronic Speed Controller (ESC)
```
```
PWM
```
```
Motors (×4)
```
```
3-Phase
```
```
Legend
Wired Data/Signal Flow
Bidirectional Wired
Wireless RF Link
Subsystem Boundary
```
```
Figure 13: High-level Drone electronics architecture and subsystem interfaces
```
##### 3.5.1.2 Rover-Mounted Landing Platform

Designed to execute the additional task within the Droning Sub-Task, the rover features a modular
mobile landing platform with a radius of 0_._ 4 m. Fabricated from aluminum alloy to ensure stability during
autonomous flight operations, the structure securely mounts to the upper chassis for rapid attachment
and removal.

#### 3.5.2 Avionics and Communications Infrastructure

##### 3.5.2.1 Core Computing and Flight Control

The flight controller handles real-time control (attitude stabilization, sensor fusion, fail-safes) and directly
processes 2_._ 4 GHzreceiver input in manual mode, while the companion computer runs heavy autonomy
tasks (computer vision, trajectory generation, state machine) and, in autonomous mode, sends motion
commands that the flight controller safety-checks before motor actuation.

##### 3.5.2.2 Radio Frequency Architecture

The Drone communication system utilizes a multi-band radio frequency (RF) architecture (Table 12)
comprising a 2_._ 4 GHzradio control (RC) link, a 5_._ 8 GHzanalog video link, and a 433 MHztelemetry


link.

##### 3.5.2.3 System Redundancy

To maximize reliability, the Drone architecture incorporates the following redundancies:

- **Sensors:** Triple-redundant IMUs in the flight controller use a voting algorithm to immediately
    isolate faulty data.
- **Communication:** A 433 MHztelemetry link backs up the primary 2_._ 4 GHzRC link (§ 3.5.2.2),
    with automatic failover verified via mid-flight signal loss testing.
- **Perception:** An onboard video switcher toggles between the Forward and Downward cameras,
    ensuring continuous visual feedback if one perspective is compromised.

#### 3.5.3 Perception and Autonomous Navigation

##### 3.5.3.1 Autonomous Navigation Pipeline

During the Droning Sub-Task, the Drone runs in fully autonomous mode. The companion computer
handles mission logic and vision processing (§ 3.5.3.3), while control commands are executed through the
architecture shown in Figure 14. Any detected anomaly triggers the relevant failsafe procedure (§ 3.7).
After start, the vehicle performs an outward search pattern; once the ArUco marker is detected, it
immediately switches to alignment and landing.
**SENSORS**

```
FLIGHT CONTROL
```
```
COMPANION COMPUTER
```
```
PiCamera
```
```
Optical Flow
```
```
GPS
```
```
IMU
```
```
Flight Controller
```
```
EKF / Sensor Fusion
```
```
Drone Motors
```
```
Companion Computer
```
```
CV / Marker Detection
```
```
Figure 14: Drone dataflow and control architecture for autonomous navigation and task execution
```
##### 3.5.3.2 Localization

The Drone utilizes an EKF to fuse Global Navigation Satellite System (GNSS), optical flow, and IMU
data into a robust, dual-layered navigation system.
Macro-navigation relies on the GNSS module for absolute global positioning. This data is strictly used to
enforce operational geofences and guarantee the reliable execution of Return-to-Launch (RTL) or Loiter
flight modes. Conversely, micro-navigation depends on the optical flow sensor to track relative local
coordinates and maintain stable hovering. This stable positioning allows the companion computer to
reliably execute precise movement commands required for autonomous target alignment.

##### 3.5.3.3 Computer Vision and Imagery

The companion computer processes a downward-facing RGB stream for real-time imagery, ArUco detection,
and relative localization. Marker pose from calibrated camera parameters is fused with flight-controller
orientation data (§ 3.5.3.2) to transform measurements into the Drone local frame. This estimate is used
to send landing commands to the flight controller, while the same pipeline detects target probes and logs
their positions relative to the start point.

### 3.6 Drone Technical Budgets

#### 3.6.1 Drone Mass Budget

The mass budget in Table 13 categorizes the Drone into dry mass, battery, and payload, with a lightweight
frame and core avionics keeping baseline mass low; a15 %engineering margin is applied to the system
subtotal to account for unmodeled items such as wiring, fasteners, and conformal coating, resulting in a
calculated MTOM of 2_._ 75 kg, which remains well below the 5_._ 0 kglimit for the Droning Sub-Task, while
propulsion calculations confirm the selected motors provide sufficient thrust for stable operation with a
safe thrust-to-weight ratio.

#### 3.6.2 Drone Power Budget

The power budget is evaluated for a single operating condition: _hover_ (propulsion with four rotors,
attitude control, and baseline electronics): _P_ hov= _P_ prop+ _P_ control _,_ avg_._
Propulsion power is estimated from induced + profile power (momentum theory adapted for multicopter


```
Table 13: Drone Mass Budget and MTOM Calculation
Category Component Estimated Mass (g)
Dry Mass Airframe, Motors & ESCs 820
Flight Controller 34
Companion Computer 105
Telemetry & RC Receiver 32
Battery Mass Battery 800
Payload & Misc. Vision Sensors, Antennas, Wiring & Misc. 600
System Subtotal 2391
Engineering Margin ( 15 % ) 359
Calculated MTOM 2750
Table 14: Hover power budget
```
```
Term Expression / basis Value
```
```
Induced power (per motor) k
√ T prop^3 /^2
2 ρA
```
###### 54. 7 W

```
Rotor solidity σ NcπR 0. 0595
Profile power (per motor) ρA ( V tip)^3 σc 8 d^018. 99 W
Mechanical rotor power P mr 4( Pi, h+ P 0 ) 294. 76 W
Propulsion power P prop P mr 294. 76 W
Control average P control , avg P control , peak D, D = 0. 05 to 0. 15 20 W(nominal)
Total hover P hov P prop+ P control , avg , nom 314. 76 W
Hover energy for60 min, E hov P hov·1 h 314. 76 W h
```
```
hover). For a quadcopter ( NR = 4) the total weight is equally shared among the rotors:
```
```
T total= mg, T prop=
```
```
T total
4
```
```
, σ =
```
```
Nc
πR
```
```
, Pi, h= k
```
```
T prop^3 /^2
√
2 ρA
```
###### ,

```
P 0 = ρA ( V tip)^3
```
```
σcd 0
8
```
```
, P mr , per= Pi, h+ P 0 , P mr= 4 P mr , per , P prop= P mr.
```
Assumptions: _m_ = 2_._ 75 kg(total vehicle mass (§ 3.6.1)), _ρ_ = 1_._ 225 kgm−^3 (sea-level air density),
_R_ = 0_._ 127 m(rotor radius per propeller), _A_ = _πR_^2 = 0_._ 0506 m^2 (disk area per rotor), _V_ tip= 118_._ 1 m s−^1
(tip speed, assumed 11100 RPM), _cd_ 0 = 0_._ 025 (blade profile drag coefficient), _k_ = 1_._ 10 to 1_._ 15 → 1_._ 1
(induced-power correction factor).
Calculated hover power is summarized in Table 14. The Drone is powered by a 5S LiPo battery, which
delivers the necessary voltage and energy capacity to successfully complete the mission.

### 3.7 Drone Safety Systems

#### 3.7.1 Failsafe Protocols

```
The flight controller operates on ArduPilot, a highly reliable open-source autopilot software that provides
robust failsafe mechanisms.
In compliance with safety requirements, if the system experiences a connection loss or detects a critical
battery voltage drop, the Drone immediately aborts its mission and executes an emergency auto-land
sequence. Additionally, a pre-defined software geofence restricts the flight volume, acting as an invisible
boundary that strictly prevents the Drone from flying beyond the designated operational area. Furthermore,
the RC transmitter is equipped with manual override switches. Toggling these switches allows the operator
to instantly interrupt autonomous operations, regain full manual control of the Drone at any moment,
and transition between different flight modes.
```
## 4 RIO Analysis

### 4.1 Methodology

The team applies a project-specific qualitative method during weekly subsystem reviews (mechanical,
electrical, software, science). For each identified risk, the risk owner defines root cause, operational impact,
and mitigation actions, then assigns **Likelihood** (L) and **Severity** (S) on a 1–5 scale.
Likelihood (probability within the current project phase) is scored as: L1 Rare ( _p <_ 10%), L2 Unlikely
(10%≤ _p <_ 30%), L3 Possible (30%≤ _p <_ 50%), L4 Likely (50%≤ _p <_ 70%), and L5 Almost certain
( _p_ ≥70%).


Severity (impact on mission readiness, safety, schedule, and compliance) is scored as: S1 Negligible (no
replanning), S2 Minor (local workaround), S3 Moderate (subsystem rework or test delay), S4 Major
(milestone slip or partial task-capability loss), and S5 Critical (safety/compliance failure or mission task
loss). Response strategy is selected per risk as _Accept_ , _Mitigate_ , _Transfer_ , or _Avoid_.

### 4.2 Qualitative Risks Assessment, Opportunities, and Issues

```
Detailed registers are provided at the end of the report in Table 21, Table 22, and Table 23.
```
## 5 Project Budget

```
The project budget is derived directly from the rover and drone product trees (Section 3.1).
```
### 5.1 Budget Summary

```
Table 15: Budget summary
```
```
Category Budget [$] Spent [$] Remaining [$]
Rover hardware (COTS + custom) 14100 3094 11006
Drone hardware 1500 542 958
Component delivery 1000 0 1000
Software / licences 800 0 800
Manufacturing / machining 800 0 800
Operational and logistics costs 5000 0 5000
Spare parts and future upgrades 6800 0 6800
Risk and contingency reserve 5000 0 5000
Total approved budget 35000 3636 31364
```
```
Table 15 includes reserves for manufacturing, logistics, spare parts, and contingency, ensuring financial
robustness during integration and testing.
```
```
Table 16: Sources of financial support
```
```
Source Amount ($) Notes
Ukrainian Catholic University 35000 supported by Nova Ukraine, SoftServe,
ELEKS, and Infineon
Total 35000
```
```
Funding sources are listed in Table 16, and the detailed product-tree budget is provided at the end of the
report in Table 20. The remaining budget is reserved for custom components, integration, software, spare
parts, and contingency.
```
### 5.2 COTS and Custom Components

```
The design uses a mixed COTS and custom approach. COTS components are selected for critical
subsystems to ensure reliability and fast integration, while custom parts are limited to structural elements
required by the rover geometry. The COTS/custom split is summarized in Table 17.
```
```
Table 17: Rover custom-manufactured components and COTS/custom cost split
Item Classification Cost ($)
TPU 3D-printed parts Chassis / Arm / Science 1000
Machining and fabrication of metal parts Chassis / Structure 800
Custom carriage / integration assemblies Mobility 500
Custom subtotal Custom 2300
COTS rover components Cost split 11800
Custom rover components Cost split 2300
Total rover hardware COTS + custom 14100
```

### 5.3 Non-Engineering Costs

```
Table 18: Operational and logistics costs
Item Cost ($) Notes
Accommodation 1729 team stay during competition
Travel to competition 951 transport to Poland
Food 1038 team meals during competition
Rover transportation 26 rover transport logistics
Return travel 778 transport back after competition
Local transportation and logistics 250 local mobility, fuel, transfers
Equipment handling and packing 228 packaging, tools, consumables
Total operational costs 5000
```
```
Table 19: Delivery costs for hardware procurement
```
```
Category Cost ($)
International shipping of electronics and sensors 635
Local delivery of mechanical parts and materials 250
Additional shipping overhead and contingencies 115
Total delivery 1000
```
### 5.4 Budget Analysis

The rover dominates the budget due to its mechanical complexity, actuation, and onboard autonomy,
with the main cost drivers being computing, mobility, and the robotic arm. COTS components are
used for critical subsystems to reduce risk and integration time, while custom parts are limited to
structural elements. The drone is a low-cost, mostly COTS-based subsystem. The remaining budget
covers manufacturing, delivery (Table 19), and non-engineering costs (Table 18), plus spare parts and
contingency, ensuring robustness within the 35,000 $ constraint.

## Appendices

**Appendix A – Requirements Table**


**Appendix C – Detailed Budget**

```
Table 20: Project budget based on the product tree
```
```
No.
```
```
High Level Subsystem
```
```
Low Level Subsystem
```
```
Part / Subassembly
```
```
Price [$]
```
```
Qty
```
```
Total [$]
```
###### 1

```
Rover
```
```
Operation and control
```
```
Main computer (Jetson Orin NX)
```
###### 2200

###### 1

###### 2200

###### 2

```
Rover
```
```
Operation and control
```
```
Navigation cameras (ArduCam + Stereo)
```
###### 200

###### 2

###### 400

###### 3

```
Rover
```
```
Communication
```
```
Wi-Fi + fallback communication system
```
###### 200

###### 1

###### 200

###### 4

```
Rover
```
```
Chassis
```
```
Structural elements (body, frame, mounts)
```
###### 500

###### 1

###### 500

###### 5

```
Rover
```
```
Drive module
```
```
Drive motors (DM-J10010L)
```
###### 221

###### 4

###### 884

###### 6

```
Rover
```
```
Drive module
```
```
Rotation motors (DM-J4340)
```
###### 260

###### 4

###### 1040

###### 7

```
Rover
```
```
Power module
```
```
Batteries + BMS
```
###### 185

###### 4

###### 740

###### 8

```
Rover
```
```
Arm
```
```
High-torque actuators
```
###### 260

###### 3

###### 780

###### 9

```
Rover
```
```
Arm
```
```
Low-torque actuators
```
###### 170

###### 3

###### 510

###### 10

```
Rover
```
```
Arm
```
```
Arm electronics (controller + camera)
```
###### 235

###### 1

###### 235

###### 11

```
Rover
```
```
Science
```
```
Exploration sensors (spectral + thermal cameras)
```
###### 700

###### 1

###### 700

###### 12

```
Rover
```
```
Science
```
```
Sampling system (drill + driver)
```
###### 70

###### 1

###### 70

###### 13

```
Rover
```
```
Science
```
```
Analysis sensors (pH, pump, microcontroller)
```
###### 200

###### 1

###### 200

###### 14

```
Rover
```
```
Navigation
```
```
Perception system (LiDAR, ToF, stereo camera)
```
###### 1036

###### 1

###### 1036

###### 15

```
Rover
```
```
Signalling
```
```
Lights, buzzer, emergency stop
```
###### 100

###### 1

###### 100

###### 16

```
Drone
```
```
Control
```
```
Flight controller (Pixhawk 6C)
```
###### 138

###### 1

###### 138

###### 17

```
Drone
```
```
Control
```
```
Companion computer (Raspberry Pi 5)
```
###### 100

###### 1

###### 100

###### 18

```
Drone
```
```
Perception
```
```
GPS + optical flow + cameras
```
###### 150

###### 1

###### 150

###### 19

```
Drone
```
```
Communication
```
```
RC + telemetry + receiver
```
###### 350

###### 1

###### 350

###### 20

```
Drone
```
```
Propulsion
```
```
Motors + ESC
```
###### 15

###### 8

###### 120

###### 21

```
Drone
```
```
Power
```
```
Battery + power electronics
```
###### 100

###### 1

###### 100

###### 22

```
Travel
```
```
Transport
```
```
Travel to competition
```
###### 951

###### 1

###### 951

###### 23

```
Travel
```
```
Accommodation
```
```
Accommodation
```
###### 1729

###### 1

###### 1729

###### 24

```
Travel
```
```
Food
```
```
Meals
```
###### 1038

###### 1

###### 1038

###### 25

```
Travel
```
```
Logistics
```
```
Miscellaneous logistics
```
###### 300

###### 1

###### 300

```
Total 1
```
```
Rover
```
###### 9395

```
Total 2
```
```
Drone
```
###### 958

```
Total 3
```
```
Other costs
```
###### 4018

```
Total 4
```
```
All above
```
###### 14371

```
Appendix D – RIO Tables
```

Table 21: Risk register (top 10)

```
ID Risk Title
```
```
Owner
```
```
Root Cause
```
```
Impact
```
```
L S RI Response Mitigation
```
```
Status
```
```
R-01 Critical subsystem
```
```
failure
```
```
Engineer
```
```
Mechanical/electrical nodefailure during competitionoperation
```
```
Functional capability loss andpotential task interruption
```
###### 4 4

```
16 Mitigate Maintain spare-parts stock
```
```
and prepared repairprocedures
```
```
Open
```
```
R-02 Transport defects Logistics
```
```
Manager
```
```
Shock and handling loads duringtransit to the competition site
```
```
Physical damage to roverassemblies before operations
```
###### 3 4

```
12 Mitigate Use palletized transport
```
```
and modular ordisassemblable packaging
```
```
Open
```
```
R-03 Overheating
```
```
HardwareEngineer
```
```
Electronics/motors under highthermal load (ambient above 30
```
###### ◦C

###### )

```
Performance degradation andreliability reduction
```
###### 3 4

```
12 Mitigate Sensor monitoring,
```
```
power-saving mode, activecooling (designed for
```
###### 40

###### ◦C

```
to
```
###### 50

###### ◦C

###### )

```
Open
```
```
R-04 Limited prior
```
```
competitionexperience
```
```
Team Lead First ERC participation and
```
```
incomplete familiarity with rulenuances
```
```
Lower execution efficiencyand increased proceduralerrors
```
###### 5 2

```
10 Accept
```
```
Regular consultations withdomain specialists andmentors
```
```
Open
```
```
R-05 Control-logic
```
```
robustness issues
```
```
Developer
```
```
Singularities and hardcoded logicpaths in autonomy/controlsoftware
```
```
Operational instability andreduced task reliability
```
###### 3 3

```
9 Mitigate Refactor control logic and
```
```
implement failsafealgorithms
```
```
Open
```
```
R-06 Hardware
```
```
incompatibility
```
```
HardwareEngineer
```
```
Interface mismatch betweencompanion computer, cameras,and sensors
```
```
Functional integration loss inperception/control pipeline
```
###### 3 3

```
9 Mitigate Perform early
```
```
cross-subsystem integrationverification
```
```
Open
```
```
R-07 Manufacturing
```
```
quality variance
```
```
Engineer
```
```
Fabricated parts deviating fromnominal dimensions/specification
```
```
Quality and fit issues duringassembly and operations
```
###### 3 3

```
9 Mitigate Prefer standard
```
```
components andtolerance-robust design
```
```
Open
```
```
R-08 Budget overrun risk Project
```
```
Manager
```
```
Cost growth or funding shortfallduring build and integration
```
```
Financial pressure affectingprocurement and schedule
```
###### 2 4

```
8 Mitigate Keep contingency reserve
```
```
and enforce strict expensetracking
```
```
Open
```
```
R-09 Preparation power
```
```
outage
```
```
Operations Grid outage during
```
```
preparation/testing activities
```
```
Schedule disruption andreduced test throughput
```
###### 2 3

```
6 Mitigate Use power banks and
```
```
pre-charged batteries forcritical work
```
```
Open
```
```
R-10 Adverse weather
```
```
conditions
```
```
Drone Pilot Strong wind and unstable
```
```
weather during outdooroperations
```
```
Reduced drone operationalenvelope and missioninterruption
```
###### 2 3

```
6 Mitigate Monitor weather forecast
```
```
and adapt mission planaccordingly
```
```
Open
```
```
Appendix E – Detailed Preliminary Test Plan
```

Table 22: Opportunities register

```
ID Opportunity
```
```
Owner
```
```
Description / Benefit
```
```
Action
```
```
O-01 New-team perspective Team Lead As a new team, we can approach design choices without legacy
```
```
constraints and propose unconventional yet effective solutions.
```
```
Prioritise fast concept validation and keep aninnovation track in design reviews.
```
```
Table 23: Issues register
```
```
ID Issue
```
```
Owner
```
```
Description / Impact
```
```
Action
```
```
Status
```
```
I-01 Time shortage
```
```
ProjectManager
```
```
Limited available time across parallel developmentstreams can delay verification and integration.
```
```
Reprioritise backlog weekly and protectintegration/test windows.
```
```
Open
```
```
I-02 Motor delivery delay
```
```
SuspensionLead
```
```
Delayed motor shipment prevents suspensionassembly start and shifts downstream integrationmilestones.
```
```
Re-sequence tasks, track suppliers daily, and preparealternate sourcing options.
```
```
Open
```
```
I-03 Burned camera module Perception
```
```
Lead
```
```
Failed camera hardware blocks early developmentand validation of vision algorithms.
```
```
Replace module, add electrical protection checks,and continue with recorded datasets in parallel.
```
```
Open
```
```
Table 24: Preliminary Test Plan
```
```
ID Test Name
```
```
Req.
```
```
Description
```
```
Pass Criteria
```
```
Suspension Team SUS-
```
###### 01

```
Turning radius test FUN-030 Turns on sand surface in both directions forward and reverse; radius of
```
```
outermost wheel-track circle measured.
```
```
Turning radius does not exceed
```
###### 0.

```
7 m
```
```
in all tested
```
```
directions.
```
###### SUS-^02

```
Water splash test
```
```
ENV-020 Fully assembled rover/drone exposed to simulated moderate rain from all
```
```
directions for 10 minutes; arm cycled through full range of motion duringexposure.
```
```
Rover, arm, and drone operate nominally afterexposure.
```
###### SUS-^03

```
Dust & mud test
```
```
ENV-030 Rover operated on dusty and muddy terrain for 30 minutes; electronics
```
```
compartments inspected for ingress after test.
```
```
All systems operate nominally after exposure.
```
###### SUS-^04

```
Wheel rigidity &terrain test
```
###### DES-130FUN-020

```
Wheel placed vertically on hard flat surface, 50 kg radial load applied atwheel centre, deformation measured; rover operated on representativeterrain types including gravel, sand, and steep slopes; wheel structuralintegrity inspected before and after each run.
```
```
No structural deformation or cracking observed; rovertraverses all terrain types including slope.
```
```
Robotic Arm Team ARM-
```
###### 01

```
Autonomous panelinterfaces actuation
```
###### DES-140; FUN-

###### 190,200,210

```
Trigger autonomous mode; CV detects panel interfaces; arm autonomouslyaligns and toggles lever and rotary switches; operate electromagnetic lockand detach; grasp, align, and fully insert IEC320 C14 plug; no teammember interacts with the ground station.
```
```
Rover successfully actuates switches, operates the lock,and inserts the plug without operator intervention andwithout panel damage.
```
###### ARM-

###### 02

```
Manualteleoperation andswipe test
```
###### DES-140; FUN-

###### 190,200,210

```
Utilize arm camera feed; operator manually aligns and toggles lever androtary switches; manually swipe the card through the lock mechanism;grasp, align, and manually insert the plug.
```
```
Operator successfully manipulates all interfaces andperforms the card swipe without panel damage.
```
###### ARM-

###### 03

```
Probing taskoperation test
```
```
DES-140 Approach the defined probe; grasp it with the gripper; transport to target
```
```
coordinates; insert into the container.
```
```
Probe successfully grasped, transported, and insertedinto the designated target.
```

**Science Team** SCI-

###### 01

```
Surface samplecollection capability
```
###### FUN-

###### 080,090,110;

###### DES-

###### 070,080,140

```
Bucket jaw scoops regolith into the correct container and weighs the depositon the onboard scale; bucket jaw grips a 15 cm rock specimen.
```
```
At least
```
```
100 g
```
```
regolith deposited into correct container;
```
```
15 cm rock secured.
```
###### SCI-^02

```
Deep samplecollection capability
```
###### FUN-130;

###### DES-090,140

```
Auger drills into analog soil (no rocks); penetration depth measured with aruler after each of 3 runs; sample weighed after collection.
```
```
Auger reaches at least
```
```
30 cm
```
```
and retains at least
```
```
100 g
```
```
of deep-soil sample in all 3 runs.
```
###### SCI-^03

```
Liquid samplecollection capability
```
###### DES-140;GEN-120

```
Intake tube submerged until bottom-contact sensor triggers; pumpactivated; tubing inspected for leaks; fill level checked after collection; pumpauto-stop confirmed at target threshold.
```
```
At least
```
###### 100

```
mL
```
```
collected into sealed vessel; no external
```
```
leakage; pump stops automatically at target fill level.
```
###### SCI-^04

```
Rock containervalidation
```
###### DES-080;FUN-080

```
Insert a rock specimen of 15 cm along its longest axis into the Rock Cup;verify fit; close lid and confirm latch engagement.
```
```
Rock specimen fits inside Rock Cup; lid closes andlatches securely.
```
###### SCI-^05

```
Regolith containervalidation
```
###### DES-070;

###### FUN-080,090

```
Transfer at least
```
```
100 g
```
```
of regolith from the bucket jaw into the Regolith
```
```
Cup; inspect all cup surfaces and seams for material leakage after deposit.
```
```
At least
```
```
100 g
```
```
regolith in cup; no leakage at any seam.
```
###### SCI-^06

```
Deep containervalidation
```
###### DES-090;

###### FUN-080,130

```
Discharge auger output into the Deep Cup opening; inspect cup and allseams for leakage after deposit.
```
```
At least
```
```
100 g
```
```
of auger output enters Deep Cup; no
```
```
leakage at any seam.
```
###### SCI-^07

```
Liquid containervalidation
```
```
GEN-110,120 Fill Astrobio container to target volume, seal it, and inspect all joints,
```
```
tubing connections, and the pH port for leakage; confirm lid and seals latchafter filling.
```
```
Container holds at least
```
###### 100

```
mL
```
```
; no leakage at any joint,
```
```
tube, or pH port; lid latches securely.
```
###### SCI-^08

```
Autonomousregolith and rockcollection
```
```
FUN-060,160 Test the autonomous surface-sampling pipeline, in which the arm camera
```
```
and gripper collect regolith and rock samples without operator input; noteam member interacts with the ground station.
```
```
Regolith at least
```
```
100 g
```
```
and rock at least 15 cm placed in
```
```
correct containers; lids latch; mass logged; no operatorintervention.
```
###### SCI-^09

```
Autonomous deepsample collection
```
###### FUN-

###### 060,130,160

```
Test the autonomous deep-sampling pipeline, in which the augerautonomously drills and deposits a soil core sample without operator input;no team member interacts with the ground station.
```
```
Auger reaches at least
```
```
30 cm
```
```
; at least
```
```
100 g
```
```
in Deep
```
```
Cup; mass logged; no operator intervention.
```
###### SCI-^10

```
Autonomoussample collectionpipeline
```
```
FUN-060,160 Test the autonomous liquid-sampling pipeline, in which the pump gripper
```
```
autonomously collects a liquid sample and stops at the fill thresholdwithout operator input; no team member interacts with the ground station.
```
```
At least
```
###### 100

```
mL
```
```
in Astrobio container; pump auto-stops;
```
```
pH logged; no leakage; no operator intervention.
```
###### SCI-^11

```
Weighing accuracy,repeatability, andtilt compensation
```
###### FUN-

###### 100,120,140

```
Place a certified 100 g calibration weight on each of the three load cells andrecord measured mass; repeat measurements while rover is on differentinclines; measured values displayed on ground station.
```
```
All readings are within 99–101 g for each container.
```
```
Navigation Team NAV-
```
###### 01

```
Full autonomoustraverse test
```
###### OPS-050; FUN-

###### 060,220,240

```
A start point and 5 ordered waypoints are provided to the system; the roverautonomously traverses across terrain with obstacles, hills, and slopes, andreturns to the starting position; no team member interacts with the groundstation.
```
```
All waypoints, including the return to start, are reachedin the correct order within
```
```
1 m
```
```
accuracy; no physical
```
```
collisions.
```
###### NAV-

###### 02

```
Pre-motion warningtiming test
```
###### OPS-

###### 080,090,100;

###### FUN-070

```
Autonomous mode is activated for the rover/drone via the ground station.
```
```
Rover/drone indicator lamp changes color and blinks forat least
```
```
5 s
```
```
upon activation; zero movement occurs
```
```
during this delay.
```

###### NAV-

###### 03

ArUco markerdetection and poseestimation test

FUN-230 ArUco markers are placed at known ground-truth locations; marker

```
detection and relative pose estimation is executed via static images and livefeeds; calculated marker positions are compared against ground truth.
```
Rover/drone calculates marker translation/orientationwith errors at most

```
5 cm
```
###### /^5

```
◦
```
```
(at
```
```
1 m
```
```
distance or less)
```
```
and at most
```
```
20 cm
```
###### /^10

```
◦
```
```
(at above
```
```
1 m
```
```
distance).
```
###### NAV-

###### 04

```
Dynamic obstacleavoidance test
```
###### FUN-240

```
Rover moves forward while another rover/obstacle approaches from varyingangles across multiple runs.
```
```
Zero collisions; rover halts at distance at least
```
```
1 m
```
```
from
```
```
the other rover.
```
###### NAV-

###### 05

```
Long-rangelocalization test
```
```
FUN-220 Rover traverses a
```
```
150 m
```
```
route; its estimated global pose and heading are
```
```
compared against ground-truth RTK GPS and precision magnetometermeasurements.
```
```
Maximum positional error is below
```
###### 0.

```
8 m
```
```
and maximum
```
```
absolute heading error is below
```
###### 8.

###### ◦ 0

```
relative to global
```
```
North across the whole run.
```
###### NAV-

###### 06

```
Low-lightconditions test
```
###### ENV-040

```
The following tests are performed in a dark environment with a predefinedlighting level: SCI-08-010; NAV-01, 03-05; ARM-01-03; DRO-02, 06, 07
```
```
The pass criteria for all specified tests are successfullymet under low-light conditions.
```
```
General Electronics Team ELE-
```
###### 01

```
60-minute missionprofile test
```
###### OPS-140;FUN-150

```
Outdoor soil terrain; rover drives figure-8 for 5 min, stops, arm movescontinuously for 5 min; repeat cycle; test ends after 60 min or batterydepletion; containers loaded before test; verify sample masses and containerstates after test.
```
```
Test duration is at least 60 minutes; mass loss of sampleis at most
```
```
5 g
```
```
per cup.
```
###### ELE-^02

```
Indicator visibilityat 10 m
```
```
DES-060 Observer is positioned at a distance of
```
```
10 m
```
```
from the rover; indicator is
```
```
activated in blinking mode; observer visually checks indicator visibility.
```
```
Blinking indicator is clearly visible from
```
```
10 m
```
###### .

###### ELE-^03

```
Max speedverification
```
```
FUN-010 Rover is commanded to move forward and reverse at maximum speed;
```
```
speed and position are measured using GPS and computed in real time bythe control system; test is performed on flat terrain and on sloped terrain.
```
```
Measured speed does not exceed
```
```
1 m s
```
```
−
```
###### 1.

```
Ground Station Team GSU-
```
###### 01

```
GS setup, failover,and E-stop test
```
###### OPS-010,OPS-020,OPS-030,OPS-060,OPS-160,DES-150,GEN-060

```
Assemble Ground Station (mast, antenna, ETH/PoE); connect Wi-Fi torover and verify drive, arm, cameras, and E-stop; disable router and confirmLoRa takeover within
```
```
10 s
```
```
, then re-enable and confirm switchback within
```
```
10 s
```
```
; connect wired controller and verify drive with no RF active; press
E-stop and verify rover stops within
```
```
1 s
```
```
, then press Start and verify
```
```
recovery; arm drone, verify RC, FPV, and MAVLink on GS, and executetakeoff, hover, and land.
```
```
Rover is controllable over Wi-Fi, LoRa, and wired links;E-stop halts rover within
```
```
1 s
```
```
with full recovery on Start;
```
```
drone RC, FPV, and MAVLink are confirmed; setupcompletes within allocated prep time.
```
###### GSU-

###### 02

```
Range,non-line-of-sight,and interferencetest
```
###### FUN-040,FUN-050,DES-110,OPS-040

```
Drive rover to
```
```
100 m
```
```
and verify
```
```
5 GHz
```
```
link; drive behind terrain obstacle
```
```
and verify link holds for at least 3 minutes; repeat both scenarios over433 MHz
```
```
LoRa only; generate traffic simulating at least four competing
```
```
teams and operate rover and drone communications simultaneously for atleast 5 minutes while verifying only declared streams are active
```
```
For both links, packet loss remains below 5% andlatency remains below
```
```
500 ms
```
```
at
```
```
100 m
```
```
with and
```
```
without LOS; no undeclared streams are detected; nocommunication dropout occurs under interference
```
###### GSU-

###### 03

```
Full function andremote imaging test
```
###### OPS-140,OPS-160,FUN-170,FUN-180

```
Drive rover across an area with test-chart letters placed up to
```
```
10 m
```
```
; operate
```
```
all rover functions from GS: drive in all directions and on slope, all cameras(cycle all feeds and capture one still photo per camera), each arm jointthrough full range, drill, science module, E-stop, and reset; identify allletters using live feeds only, without prior knowledge
```
```
All rover functions respond correctly; packet lossremains below 5%, latency remains below
```
```
500 ms
```
```
, and
```
```
no dropout occurs; all feeds become live within
```
```
3 s
```
```
without restart; one still photo is saved per camera; allletters are correctly identified and screenshots are logged
```
```
Drone Team
```

###### DRO-

###### 01

```
Hot/coldenvironmentalfunctionality test
```
###### ENV-010

```
Place drone and rover in a temperature chamber; soak at
```
###### 30

###### ◦C

```
and
```
###### 0

###### ◦C

```
for
```
```
30 minutes; verify full functionality (teleoperation, sensors, actuators,communication, and autonomy indicators).
```
```
Drone and rover maintain full functionality (control,telemetry, video, movement, and indicators) after30-minute exposure to both
```
###### 30

###### ◦C

```
and
```
###### 0

###### ◦C

###### .

###### DRO-

###### 02

```
Autonomous searchand vision test
```
###### FUN-060;OPS-050

```
Command autonomous grid search with downward LED and autonomyindicator lamp active; use HDR camera processing; detect ArUco markersvia CV pipeline; no team member interacts with the ground station
```
```
Autonomy indicator lamp remains visible withoutblinding cameras; stable position hold with no drift viaoptical flow plus LED; all ArUco markers continuouslydetected; no operator intervention
```
###### DRO-

###### 03

```
Failsafe test
```
```
OPS-070 Maintain stable connection with Ground Station (GS); disconnect GS link
```
```
from drone mid-maneuver to simulate total communication loss; observeemergency auto-land.
```
```
Drone immediately performs safe emergency auto-landupon total communication loss.
```
###### DRO-

###### 04

```
Equipment failsafetest
```
```
GEN-070 Remotely steer and control the drone using an additional RC system and
```
```
maintain communication through this backup control link.
```
```
RC system successfully steers and controls the droneand maintains stable communication.
```
###### DRO-

###### 05

```
In-flight hardwareredundancy test
```
```
DES-150 Secure drone on test bench (propellers removed); disable primary IMU in
```
```
real time; monitor Extended Kalman Filter (EKF) voting and attitude data;reinstall propellers and command autonomous waypoint flight.
```
```
EKF instantly switches to redundant IMUs with no lossof stability or orientation.
```
###### DRO-

###### 06

```
Localization test
```
```
FUN-220 Drone flies to a known position from lift-off; compute relative pose using
```
```
IMU, optical flow, and GPS; compare calculated X/Y positions to groundtruth
```
```
Relative position error is at most 5% versus groundtruth
```
###### DRO-

###### 07

```
Collision avoidancetest
```
```
FUN-240 Drone flies forward toward an obstacle.
```
```
Drone detects obstacle and stops at least
```
```
1 m
```
```
away
```
```
without collision.
```
```
Appendix F – Product Trees
```
```
Control
```
```
Propulsion
```
```
Structure
```
```
Power
```
```
Perception
```
```
Communication
```
```
Drone
```
```
Flight controller•
Pixhawk 6C
Companion computer•
Raspberry Pi 5
GPS & Compass•
Holybro M10 GPSmodule
Optical flow•
MicroAir MTF-01
```
```
ESCMotors•
DJI 2212 920KVbrushless motors
Propellers
```
```
Frame•
F450
Landing gearPropeller guards
```
```
Battery•
LiPo
DC-DC convertersPower module
```
```
Forward camera•
Foxeer Cat 4 Micro
Downward CV camera•
Arducam IMX70812MP HDR
Video transmitter•
AKK Race Ranger5.8GHz
Video switcher
```
```
RC receiver•
RP1 V2 ExpressLRS 2.4GHzNano Receiver
RC controller•
TX16S
Telemetry module•
B-CUBE V5 433 MHz RadioTelemetry
Ground station
```
```
Figure 15: Drone Product Tree detailing primary subsystems and hardware components.
```

```
Power Module
```
**System**

```
HousingBatteries + BMS•48V 36-48Ah
```
```
Navigation
```
```
Lidar•RPLIDAR S2Human presence sensor•HLK-LD2450 HumanTracking RadarToF camera•Maix Sense A010ToFStereo camera•StereoLabs ZED 2i
```
```
Signalling System
```
```
Main LightsEmergency StopIndicator TowerBrightness SensorBuzzer
```
```
Chassis
```
```
Body Suspension Drive Module
```
```
FramePanelsArm Bracket
Central AxisRockersDifferential Hub FrameDrive Motor•
```
```
DM-J10010LRotation Motor•DM-J4340Wheel
```
```
Operationand control
```
```
Main computer•NVIDIA Jetson OrinNX 16GB Video subsystem Communication subsystem
```
```
Nav camera•ArduCam AR0234Main Nav Camera•ArduCam StereoAR0234
```
```
Wi-Fi Adapter (mast)•Alfa AWUS036ACHFallback antenna
```
```
Science
```
```
Exploration System
```
```
Liquid Analysis System
```
```
Sampling System
```
```
Spectral camera•MAPIR Survey3WOCNThermal camera•CADDX FPVECLIPSE 640SH +Caddx Avatar GTVTX
```
```
Container unit
```
```
Sample collection gripper
```
```
ContainerTensor sensorContainer microcon-troller•ESP32-WROOM-32D devkitLid motor•MG996R
```
```
Gripper mechanizmDrill motor•DC RS-775SHDrill driver•BTS7960 H-bridge
```
```
Astrobio microcontroller•ESP32-WROOM-32D devkitGripper mechanismLiquid pumpPump driverLiquid level sensor•XKC-Y25-NPNpH-sensor•Grove pH SensorE-201C-BlueGround sensor
```
```
Arm
```
```
Arm controller•Raspberry Pi 4 (8GBRAM)Arm camera•Arducam AR0234USB 3.0 Base Manipulation
```
```
Maintenance
```
```
High-torque planetaryactuator•
SteadyWinGIM8115-36Planetary ReducerMotor
Mounting platform
```
```
High-torque planetaryactuator•SteadyWinGIM8115-36Planetary ReducerMotorLow-torque planetaryactuator•DAMIAODM-J4340-2ECTubesJoints
```
```
Gripper mechanismGripper’s stepper motor•Nema17 TBDLoad sensor
```
```
Figure 16: Product tree
```

