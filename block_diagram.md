# Automatic Rat Aquamation Machine - Block Diagram

```mermaid
flowchart TD
    %% Layer 1: Mouse Trap
    subgraph L1["🎯 LAYER 1: MOUSE TRAP"]
        direction LR
        A["① Webcam + YOLO<br/>Detect rat"] --> B["② Servo Motor<br/>Open trap door"]
        B --> C["③ Load Cell HX711<br/>Verify weight"]
        C --> D["④ Stepper Motor<br/>Drop to L2"]
    end
    
    %% Layer 2: Electric Shock  
    subgraph L2["⚡ LAYER 2: ELECTRIC SHOCK"]
        direction LR
        E["⑤ Motion Sensor x2<br/>Detect movement"] --> F["⑥ Metal Cage<br/>Contain specimen"]
        F --> G["⑦ SSR Relay<br/>Activate shock"]
        G --> H["⑧ Stepper Motor<br/>Drop to L3"]
    end
    
    %% Layer 3: Aquamation Chamber
    subgraph L3["💧 LAYER 3: AQUAMATION CHAMBER"]
        direction LR
        I["⑨ Brass Ball Valve<br/>Release fluid"] --> J["⑩ SSR + Heater<br/>Heat liquid"]
        J --> K["⑪ MAX6675 Temp<br/>Monitor heat"]
        K --> L["⑫ Linear Actuator 1000N<br/>Push door seal"]
        L --> M["⑬ Rubber Gasket<br/>Airtight seal"]
    end
    
    %% Sequential flow between layers
    D -- "DROP" --> E
    H -- "TRANSFER" --> I
    
    %% Control System
    subgraph CTRL["🎛️ CONTROL SYSTEM"]
        direction LR
        N["⑭ LCD 3.5&quot; Display"]
        O["⑮ Emergency Stop"]
        P["⑯ Power Supply 12V 15A"]
        Q["⑰ Plywood Casing"]
    end
    
    %% Control connections
    CTRL ---|"Control"| L1
    CTRL ---|"Control"| L2
    CTRL ---|"Control"| L3
    
    style L1 fill:#e3f2fd,stroke:#1976d2,stroke-width:2px
    style L2 fill:#ffebee,stroke:#d32f2f,stroke-width:2px
    style L3 fill:#e8f5e9,stroke:#388e3c,stroke-width:2px
    style CTRL fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px
```

---

## Component Sequence Table

| Step | Layer | Component | Function |
|------|-------|-----------|----------|
| ① | L1 | Webcam + Raspberry Pi + YOLO | Detect rat entry |
| ② | L1 | Servo Motor | Open/close trap door |
| ③ | L1 | Load Cell + HX711 ADC | Weight verification |
| ④ | L1 | Stepper Motor | Transfer to Layer 2 |
| ⑤ | L2 | Motion Sensor (2x) | Detect cage movement |
| ⑥ | L2 | Metal Cage | Containment chamber |
| ⑦ | L2 | Solid State Relay | Activate electrocution |
| ⑧ | L2 | Stepper Motor | Transfer to Layer 3 |
| ⑨ | L3 | Brass Ball Valve | Regulate fluid flow |
| ⑩ | L3 | SSR + Heating Element | Heat processing liquid |
| ⑪ | L3 | MAX6675 Thermocouple | Temperature monitoring |
| ⑫ | L3 | BTS7960 + Linear Actuator 1000N | Push door for seal |
| ⑬ | L3 | Rubber Gasket | Airtight door seal |
| ⑭ | Control | LCD 3.5" + Touch Screen | Display & interface |
| ⑮ | Control | Emergency Stop Button | Shutdown |
| ⑯ | Control | Power Supply 12V 15A | Main power |
| ⑰ | Support | Plywood Casing 1/2" | Housing structure |
