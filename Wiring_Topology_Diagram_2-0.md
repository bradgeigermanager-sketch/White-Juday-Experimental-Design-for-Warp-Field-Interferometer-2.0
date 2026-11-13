flowchart TD
    classDef laser fill:#E3F2FD,stroke:#1E88E5,stroke-width:1px,color:#0D47A1;
    classDef optics fill:#E8F5E9,stroke:#43A047,stroke-width:1px,color:#1B5E20;
    classDef detector fill:#FFF3E0,stroke:#FB8C00,stroke-width:1px,color:#E65100;
    classDef electronics fill:#F3E5F5,stroke:#8E24AA,stroke-width:1px,color:#4A148C;
    classDef environment fill:#FBE9E7,stroke:#E64A19,stroke-width:1px,color:#BF360C;

    subgraph LSR["Laser Source"]
        L["632.8 nm Ultra-stable He-Ne Laser"]
    end

    subgraph OPT["Optical Interferometer"]
        BS["50:50 Mach-Zehnder Beam Splitter"]
        EXP["Experimental Arm<br/>High-Electric-Field Curvature Ring<br/>30 m Compensating Delay Fiber"]
        REF["Control Arm<br/>Reference Path<br/>Equivalent Optical Path Length"]
        PBS1["Polarizing Beam Splitter 1"]
        PBS2["Polarizing Beam Splitter 2"]
        PD1["Low-Noise Photodetector 1"]
        PD2["Low-Noise Photodetector 2"]
    end

    subgraph SIG["Signal Processing"]
        DIFF["Ultra-Low-Noise Instrumentation Op-Amp<br/>(Differential Input)"]
        LI["Digital Lock-In Amplifier<br/>Synchronized to 1 kHz Modulation Reference"]
        BOX["Boxcar Integrator<br/>10,000-Cycle Synchronous Accumulation"]
        TDC["High-Precision Time-to-Digital Converter"]
        HOST["Industrial Control Host<br/>72-Hour Continuous Data Storage"]
    end

    subgraph ENV["Mechanical & Thermal Stability"]
        ISO["Two-Stage Active Seismic Isolation Platform"]
        BREAD["ULE Optical Breadboard"]
        TEMP["Closed-Loop Temperature Control System<br/>for the Entire Enclosure"]
    end

    MOD["1 kHz Square-Wave Modulation Source"] --> EXP
    MOD -. "Reference input" .-> LI

    L --> BS
    BS --> EXP
    BS --> REF
    EXP --> PBS1
    REF --> PBS2
    PBS1 --> PD1
    PBS2 --> PD2
    PD1 --> DIFF
    PD2 --> DIFF
    DIFF --> LI
    LI --> BOX
    BOX --> TDC
    TDC --> HOST

    ISO --> BREAD
    TEMP --> BREAD
    BREAD --> BS
    BREAD --> EXP
    BREAD --> REF
    BREAD --> PBS1
    BREAD --> PBS2
    BREAD --> PD1
    BREAD --> PD2

    class L laser
    class BS,EXP,REF,PBS1,PBS2,PD1,PD2 optics
    class DIFF,LI,BOX,TDC,HOST detector
    class ISO,BREAD,TEMP environment
