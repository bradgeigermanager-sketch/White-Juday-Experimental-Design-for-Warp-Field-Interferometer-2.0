```mermaid
flowchart LR
    %% Global Grounding System
    subgraph GND["Independent Grounding System"]
        Z["Independent Grounding Electrode<br/>Ground Resistance ≤ 0.5 Ω"]
    end

    Z -- "16 mm² stranded copper wire" --> SG["Signal Ground (SG)<br/>Single-point connection to the ground terminal of the differential operational amplifier"]
    Z -- "10 mm² copper wire" --> PE["Protective Earth (PE)<br/>Star-configured distribution to power grounds of all equipment"]
    Z -- "10 mm² copper wire" --> EG["Shielding Ground (EG)<br/>Equipotential ring connected to all shielding enclosures"]

    %% Optical Link Connections
    A["632.8 nm Ultra-stable He-Ne Laser"] -- "Single-mode polarization-maintaining fiber" --> B["50:50 Mach-Zehnder Beam Splitter"]
    B --> C["Experimental Beam Path<br/>High-electric-field curvature ring + 30 m compensating delay fiber"]
    B --> D["Control Beam Path<br/>Reference optical path with equivalent optical length"]
    C --> E["Polarizing Beam Splitter 1"]
    D --> F["Polarizing Beam Splitter 2"]
    E -- "FC/APC fiber connector" --> G["Low-noise Photodetector 1"]
    F -- "FC/APC fiber connector" --> H["Low-noise Photodetector 2"]

    %% Weak-signal Differential Link Connections
    G -- "Double-shielded ZR-KVVRP twisted-pair cable" --> N["Ultra-low-noise instrumentation amplifier, IN+ terminal"]
    H -- "Double-shielded ZR-KVVRP twisted-pair cable" --> N2["Ultra-low-noise instrumentation amplifier, IN- terminal"]

    N -. "Inner shield connected to SG at the amplifier end only" .-> SG
    N2 -. "Inner shield connected to SG at the amplifier end only" .-> SG
    N -. "Outer shield connected to EG throughout the entire run" .-> EG
    N2 -. "Outer shield connected to EG throughout the entire run" .-> EG

    %% Modulation and Signal Processing Link Connections
    Q["1 kHz Square-wave Modulation Source"] -- "High-permeability Permalloy-shielded cable" --> FQ["Power input for high-electric-field curvature ring"]
    Q -- "Coaxial cable for synchronous triggering" --> J["Digital Lock-in Amplifier<br/>REF terminal"]
    N -- "Low-noise coaxial cable" --> J
    N2 -- "Low-noise coaxial cable" --> J
    J -- "Shielded cable" --> K["Boxcar Integrator<br/>10,000-cycle synchronous accumulation"]
    K -- "Shielded cable" --> L["High-precision Time-to-Digital Converter"]
    L -- "USB 3.0 shielded cable" --> M["Industrial Control Host"]

    %% Environmental Isolation System Wiring
    O["Two-stage active seismic isolation platform"] -- "Shielded power cable" --> PE
    T["Full-enclosure closed-loop temperature control system"] -- "Shielded power cable" --> PE
    S["ULE (Ultra-Low Expansion) optical breadboard"] -- "Metal braided strap" --> EG
    FC["Faraday cage metal enclosure"] -- "Conductive foam interface" --> EG

    %% Feedthrough Filtering
    U["Pi-type power filter"] -- "Power input line" --> PEP["Power entry point on Faraday cage wall"]
    V["Ferrite bead/ring"] -- "Signal input line" --> SEP["Signal entry point on Faraday cage wall"]

    %% Physical Isolation
    subgraph FaradayCage["Faraday Cage (Fully Enclosed Enclosure)"]
        direction TB

        subgraph HV["High-Voltage Modulation Chamber"]
            Q
            FQ
        end

        subgraph WeakSig["Weak-Signal Detection Chamber"]
            A
            B
            C
            D
            E
            F
            G
            H
            N
            N2
        end

        subgraph DataAcq["Data Acquisition Chamber"]
            J
            K
            L
            M
        end

        W["Grounded metal partition"] -- "Physical isolation" --> X["Between High-Voltage Modulation Chamber and Weak-Signal Detection Chamber"]
    end
```
