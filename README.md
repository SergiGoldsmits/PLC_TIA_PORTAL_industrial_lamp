# PLC_TIA_PORTAL_industrial_lamp
PLC-based lamp control with timer and counter - TIA Portal project
# Industrial Lamp Control System

PLC-based lamp control with auto-shutoff timer and usage lockout counter. This allows us to turn off the lamp before timer expires and lock out the ON state.

## Features
- Start/Stop button control with seal-in circuit
- Auto-turn off after 5 seconds (configurable timer)
- Usage counter - locks out after 2 activations
- Reset function to restore operation
- Multi-language implementation (LAD, FBD, SCL)
  

## Hardware
- Siemens S7-1200 CPU 1212C AC/DC/Rly
- Simulated in S7-PLCSIM V19
- FactoryIO

## I/O List
| Tag Name | Address | Type | Description |
|---|---|---|---|
| Start_Button | %I0.0 | Bool | Push button to start lamp |
| Count_Button | %I0.2 | Bool | Increments usage counter |
| Count_Reset | %I0.1 | Bool | Resets counter to zero |
| Lamp_On | %Q0.0 | Bool | Output lamp |
| ButtonOff | %M0.1 | Bool | TRUE when count reaches 5 / turns off lamp circuit|
| ButtonOff2 | %M0.2 | Bool | TRUE when timer  5s / turns off lamp circuit|

## Logic Description
1. Press Start_Button → Lamp turns ON
2. Timer counts 5 seconds → Lamp auto-shutoff
3. Each activation increments counter
4. After 2 activations → Count_Done blocks lamp
5. Press Count_Reset → Counter resets, lamp enabled again

## Implementation Languages
- **LAD (Ladder Logic)** - Main implementation in OB1
- **FBD (Function Block Diagram)** - Alternative in FC2
- **SCL (Structured Text)** - Basic seal-in in FB_Lamp_SCL

## How to Run
1. Open TIA Portal V19
2. Import project archive: `Lamp_Control_TIA_V19.zap19`
3. Compile project (Ctrl+B)
4. Start S7-PLCSIM V19
5. Download to PLCSIM
6. Go online and test using SIM table

## Network Descriptions
**Network 1:** Seal-in start/stop circuit with timer and counter lockout  
**Network 2:** Counter circuit - tracks lamp activations

## Notes
- Buttons use %I addresses for production compatibility
- Timer preset value: T#5S (adjustable in Data_block_1)
- Counter preset value: 5 cycles (adjustable via PV parameter)

## Future Enhancements
- Factory IO 3D visualization (requires PLCSIM Advanced or Modbus bridge)
- HMI screen with WinCC
- Analog input scaling for variable timer duration

## Author
Sergi Goldsmits
Automation Engineering Portfolio  
[16/05/2026]
