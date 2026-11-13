```mermaid
graph TD
    A[632.8 nm Ultra-stable He-Ne Laser] --> B[50:50 Mach-Zehnder Beam Splitter]
    B --> C[Experimental Arm: High-Electric-Field Curvature Ring + 30 m Compensating Delay Fiber]
    B --> D[Control Arm: Reference Path with Equivalent Optical Path Length]
    C --> E[Polarizing Beam Splitter 1]
    D --> F[Polarizing Beam Splitter 2]
    E --> G[Low-Noise Photodetector 1]
    F --> H[Low-Noise Photodetector 2]
    G --> I[Ultra-low-noise Instrumentation Op-Amp {Differential Input}]
    H --> I
    I --> J[Digital Lock-in Amplifier (Synchronized to 1 kHz Modulation Reference)]
    J --> K[Boxcar Integrator {10,000-cycle Synchronous Accumulation}]
    K --> L[High-Precision Time-to-Digital Converter]
    L --> M[Industrial Control Host {72-hour Continuous Data Storage}]
    N[Two-stage Active Seismic Isolation Platform] --> O[ULE {Ultra-Low Expansion} Optical Breadboard]
    P[Closed-loop Temperature Control System for the Entire Enclosure] --> O
    O --> [Supports All Optical Components]
    Q[1 kHz Square-Wave Modulation Source] --> [High-Electric-Field Curvature Ring]
    Q --> J[Digital Lock-in Amplifier {Reference Input}]
```
