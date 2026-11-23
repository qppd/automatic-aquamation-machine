# Automatic Rat Aquamation Machine - Block Diagram

```mermaid
flowchart TD
    subgraph L1["Layer 1: Mouse Trap"]
        direction LR
        A["1. Camera+YOLO Detect"] --> B["2. Servo Door Open"]
        B --> C["3. Load Cell Weight"]
        C --> D["4. Stepper Drop"]
    end
    
    subgraph L2["Layer 2: Electric Shock"]
        direction LR
        E["5. Motion Sensor x2"] --> F["6. Metal Cage"]
        F --> G["7. SSR Electrocut."]
        G --> H["8. Stepper Drop"]
    end
    
    subgraph L3["Layer 3: Aquamation Chamber"]
        direction LR
        I["9. Brass Ball Valve"] --> J["10. SSR Heater"]
        J --> K["11. MAX6675 Temp"]
        K --> L["12. Linear Actuator 1000N Seal"]
    end
    
    D -- "DROP" --> E
    H -- "TRANSFER" --> I
    
    subgraph CTRL["Control System"]
        direction LR
        N["13. LCD 3.5 inch Display"]
        O["14. Emergency Stop"]
        P["15. Power Supply 12V 15A"]
    end
    
    CTRL ---|"Control"| L1
    CTRL ---|"Control"| L2
    CTRL ---|"Control"| L3
```

---

## Component Sequence Table

| Step | Layer | Component | Function |
|------|-------|-----------|----------|
| 1 | L1 | Webcam + Raspberry Pi + YOLO | Detect rat entry |
| 2 | L1 | Servo Motor | Open/close trap door |
| 3 | L1 | Load Cell + HX711 ADC | Weight verification |
| 4 | L1 | Stepper Motor | Transfer to Layer 2 |
| 5 | L2 | Motion Sensor (2x) | Detect cage movement |
| 6 | L2 | Metal Cage | Containment chamber |
| 7 | L2 | Solid State Relay | Activate electrocution |
| 8 | L2 | Stepper Motor | Transfer to Layer 3 |
| 9 | L3 | Brass Ball Valve | Regulate fluid flow |
| 10 | L3 | SSR + Heating Element | Heat processing liquid |
| 11 | L3 | MAX6675 Thermocouple | Temperature monitoring |
| 12 | L3 | BTS7960 + Linear Actuator 1000N | Push door for seal |
| 13 | Control | LCD 3.5" + Touch Screen | Display & interface |
| 14 | Control | Emergency Stop Button | Shutdown |
| 15 | Control | Power Supply 12V 15A | Main power |
