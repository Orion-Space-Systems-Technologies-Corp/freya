Project Velocity: High-Performance Autonomous Logistics Platform

Fig 1: The "Sprint-Delivery" Variant. Aerodynamic, enclosed cargo pod built on a professional Lando Norris (LN) Four racing chassis.

1. Executive Summary: The "Goldilocks" Thesis

The Problem: Current last-mile solutions are fundamentally mismatched to the task.

Vans (Tesla/Rivian): Thermodynamic overkill. Moving a 2,000kg vehicle to deliver a 5kg payload is inefficient, dangerous to pedestrians, and causes congestion.

Drones: Limited payload capacity (cannot carry groceries), noise pollution, and strict airspace regulation.

The Solution: An autonomous agent engineered for the world we actually live in—a world paved for wheels.

Form Factor: "Knee-height" electric kart (Side-walk and Bike-lane capable).

Hardware DNA: Professional racing grade (OTK Group / Tony Kart).

Philosophy: Sprint Delivery. We utilize high-performance hardware for rapid transit and fast turnaround, relying on a Hot-Swap Architecture rather than heavy, long-range batteries.

2. The Business Case & Unit Economics

Our economic advantage lies in the Swarm Multiplier. We are not just replacing a driver; we are changing the ratio of labor to delivery volume.

2.1 Unit Economics Comparison

Metric

Human Courier (Van/Car)

Project Velocity (Swarm Model)

Impact / Delta

Asset Cost (CapEx)

~$45,000 (Van + Upfit)

~$3,500 - $5,000 (Target)

90% Lower CapEx

Labor Cost (Hourly)

~$20.00 / hour (1 Driver)

~$0.40 / hour (1 Operator / 50 Bots)

98% Labor Savings

Energy Efficiency

~250 Wh/mile

~35 Wh/mile

7x More Efficient

Idle Cost

High (Driver paid to wait)

Zero (Robot waits at hub)

Higher Margins

Liability Risk

High (2-ton vehicle)

Low (<50kg vehicle)

Lower Insurance

2.2 The "Swarm" Operational Flow

graph LR
    A[Logistics Hub] -- Fresh Battery + Cargo --> B(Deployed Kart)
    B -- 25km/h --> C{Routing Logic}
    C --> D[Drop 1: Pizza]
    C --> E[Drop 2: Parcel]
    C --> F[Drop 3: Medicine]
    D & E & F --> G(Return to Base)
    G -- Depleted Battery --> A
    style A fill:#f9f,stroke:#333,stroke-width:2px


3. Hardware Architecture

3.1 Chassis & Propulsion

Base Platform: Lando Norris (LN) Four Chassis (OTK Group).

Modifications: Removal of fuel tank/ICE mounts; addition of sensor/compute rigorous mounting points.

Motor: 96V PMAC (Permanent Magnet AC).

Spec: ~20kW Continuous / ~35kW Peak.

Mount: Direct Rear Axle (Inline) via custom CNC aluminum clamps.

Transmission: Direct Drive (Single Gear). Optimized for torque/acceleration to handle payload weight (~50kg).

Brakes: Hydraulic rear disc brakes (standard OTK) actuated via linear servo (Drive-by-Wire).

3.2 The "Sprint" Battery Strategy

We deliberately avoid large, heavy endurance batteries to maintain agility and payload capacity. The kart runs 24/7; only the batteries sleep.

Spec: 96V Nominal, ~50Ah (~4.8 kWh).

Chemistry: NMC (High Discharge) or LiFePO4 (Safety focus).

Form Factor: Rectangular/Flat pack, optimized for side-pod or rear mounting.

Integration: Hot-Swappable. The pack connects via quick-release Anderson SB350 connectors.

3.3 Payload: The "Smart Drawer"

The rear cargo bay utilizes a sliding drawer mechanism with internal compartmentalization to enable multi-stop delivery runs.

Mechanism: Rear Slide-Out Drawer.

Capacity: Modular (e.g., 3x Grocery Bags or 1x Large Parcel).

Security: 3x Internal Locking Segments controlled by the Jetson.

UX: Customer scans QR Code on the chassis $\rightarrow$ Specific segment unlocks $\rightarrow$ Customer retrieves goods.

4. Systems & Safety Topology

4.1 High Voltage Safety Loop (The Kill Chain)

Before the vehicle moves, the hardware safety loop must be closed. Software cannot override a broken physical loop.

flowchart TD
    A[96V Battery] --> B{Manual E-Stop Rear}
    B --> C{Manual E-Stop Side}
    C --> D{Remote Kill Switch}
    D --> E{BMS Health Check}
    D --> F{HVIL (Interlock Loop)}
    E & F -- All Pass --> G[Main Contactor CLOSES]
    E & F -- Fail --> H[System Open / Safe State]
    G --> I[Motor Controller]


4.2 Compute & Sensor Stack

Core Compute: NVIDIA Jetson Thor (or Orin AGX).

Vision: 4x Wide Angle Cameras (360° Perception).

Depth: Solid State LiDAR (Front) + Stereoscopic Depth Cameras.

Localization: GNSS/RTK Module + IMU.

Comms: 5G/LTE Module + V2X (Vehicle-to-Everything) ready.

5. Software Roadmap

Phase 1: Drive-by-Wire

Goal: Control the kart via Xbox Controller through the Jetson.

Stack: Python script translating Joystick inputs $\rightarrow$ CAN Bus frames $\rightarrow$ Motor Controller.

Phase 2: Shadow Mode

Goal: Data collection and model validation.

Action: Human operates the kart remotely. The AI runs in the background, predicting steering angles. We compare AI predictions vs. Human reality to train the model without risk.

Phase 3: Autonomy (RL)

Goal: Full Self-Driving in geofenced zones.

Stack: ROS 2 (Robot Operating System), NVIDIA Isaac Sim for synthetic training.

Policy: End-to-End Reinforcement Learning (Pixels $\rightarrow$ Control) vs. Modular Pipeline.

6. Manufacturing Workflow

De-ICE-ing: Strip Rotax engine, fuel tank, radiator, and exhaust from the LN Chassis.

Structural Mounts: Install CNC Aluminum mounts for Battery Box (Side/Rear) and Compute Unit (Center).

Propulsion: Install PMAC motor and tension the drive chain/belt.

Wiring Harness: Route HV cables (Left Side) and LV Signal cables (Right Side) to prevent interference. Install E-Stops.

Payload Integration: Mount the rear "Smart Drawer" sliding mechanism.

Bodywork: Install the "Silver Pod" aerodynamic shell.

Commissioning: Bench test HV safety loop and CAN bus communication.

7. Logistics & "Balance of System"

The Hub: Central depot for battery charging and payload loading.

Turnaround Time: Target <2 minutes for Battery Swap + Cargo Load.

Regulatory Strategy: Lobbying for "Personal Delivery Device" (PDD) classification to legalize operation on sidewalks and bike lanes.

Note to Engineers: This platform is a hybrid of F1 technology (chassis/battery discharge) and Logistics Reliability (swappable power/rugged perception). Do not compromise performance for utility; we are building the fastest, most efficient delivery robot on earth.
