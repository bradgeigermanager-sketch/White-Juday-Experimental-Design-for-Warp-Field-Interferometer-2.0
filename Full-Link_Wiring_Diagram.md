```mermaid
flowchart LR
%% Global Grounding System
subgraph Independent Grounding System
Z[Independent Grounding Electrode, Ground Resistance ≤ 0.5Ω]
end
Z --16mm² stranded copper wire--> SG[Signal Ground (SG) - Single-point connection to the ground terminal of the differential operational amplifier]
Z --10mm² copper wire--> PE[Protective Earth (PE) - Star-configured distribution to the power grounds of all equipment]
Z --10mm² copper wire--> EG[Shielding Ground (EG) - Equipotential ring connected to all shielding enclosures]

%% Optical Link Connections
A[632.8nm Ultra-stable He-Ne Laser] --Single-mode polarization-maintaining fiber--> B[50:50 Mach-Zehnder Beam Splitter]
B --> C[Experimental Beam Path: High-electric-field curvature ring + 30m compensating delay fiber]
B --> D[Control Beam Path: Reference optical path with equivalent optical length]
C --> E[Polarizing Beam Splitter 1]
D --> F[Polarizing Beam Splitter 2]
E --FC/APC fiber connector--> G[Low-noise Photodetector 1]
F --FC/APC fiber connector--> H[Low-noise Photodetector 2]

%% Weak-signal Differential Link Connections
G --Double-shielded ZR-KVVRP twisted-pair cable--> N[Ultra-low-noise instrumentation amplifier, IN+ terminal]
H --Double-shielded ZR-KVVRP twisted-pair cable--> N[Ultra-low-noise instrumentation amplifier, IN- terminal]
N --Inner shield connected to SG at the amplifier end only--> SG
N --Outer shield connected to EG throughout the entire run--> EG

%% Modulation and Signal Processing Link Connections
Q[1kHz Square-wave Modulation Source] --High-permeability Permalloy-shielded cable--> FQ[Power input for high-electric-field curvature ring]
Q --Coaxial cable for synchronous triggering--> J[Digital Lock-in Amplifier, REF terminal]
N --Low-noise coaxial cable--> J[Digital Lock-in Amplifier, SIG Input]
J --Shielded cable--> K[Boxcar Integrator, 10,000-cycle synchronous accumulation]
K --Shielded cable--> L[High-precision Time-to-Digital Converter]
L --USB 3.0 shielded cable--> M[Industrial Control Host]

%% Environmental Isolation System Wiring
O[Two-stage active seismic isolation platform] --Shielded power cable--> PE
T[Full-enclosure closed-loop temperature control system] --Shielded power cable--> PE
S[ULE (Ultra-Low Expansion) optical breadboard] --Metal braided strap--> EG
FC[Faraday cage metal enclosure] --Conductive foam interface--> EG

%% Feedthrough Filtering
U[Pi-type power filter] --Power input line--> Power entry point on Faraday cage wall
V[Ferrite bead/ring] --Signal input line--> Signal entry point on Faraday cage wall
%% Physical Isolation: High-Voltage vs. Low-Voltage/Signal Sections
style 高压调制舱 fill:#ffeeee,stroke:#ff6666,stroke-width:2px
style 弱信号探测舱 fill:#eeffee,stroke:#6666ff,stroke-width:2px
style 数据采集舱 fill:#eeeeff,stroke:#6666ff,stroke-width:2px
subgraph Faraday Cage (Fully Enclosed Enclosure)
direction TB
subgraph High-Voltage Modulation Chamber
Q
FQ
end
subgraph Weak-Signal Detection Chamber
A
B
C
D
E
F
G
H
N
end
subgraph Data Acquisition Chamber
J
K
L
M
end
W[Grounded metal partition] --Physical isolation--> Between High-Voltage Modulation Chamber and Weak-Signal Detection Chamber
end
