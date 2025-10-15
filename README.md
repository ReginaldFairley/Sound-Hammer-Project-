# Sound-Hammer-Project Version 1.0
## Description
The Fabrication Sound Hammer is an interactive impact-responsive device that combines sound, light, and motion detection to create a dynamic experience. Designed for durability and interactivity, the hammer integrates electronic sensors, microcontroller-based logic, and programmable behavior into a functional, structurally reinforced design

Line 132 indicates where I personally ended

## Material in Repository
**Power Schematic** - Ki-Cade Schematic file on how the power should work for the hammer

**3D Model of Hammer** - Fusion Autodesk 

**Arduino** - LEDs respond to impact intensity

## Hardware Components
GUIDE: Component's Purpose / Example of commponent
_(Research what works best for you personally)_

1. Microcontroller / Arduino Nano Every →
*Controls sensors, LEDs, sound*

2. Impact Sensor / LSM6DSV32XTR (LGA-14) →
*Detects motion and impact*

3. Audio Output / Piezo Buzzer →
*Responds to impact force*

4. LED Feedback / LEDS (Any Color or Quantity) →
*Lights up upon impact*

### -- Power Supply --
  
5. Rechargeable power source / Li-Po Battery (3.7V 450 mAh) →
*Powers entire system*

6. Charging circuit / Linear Battery Charger (1-cell, 8-pin IC) →
*Connects to USB-C port*

7. (Optional)Voltage regulator(if powering 5V LEDs from 3.7V battery) / Boost Converter (5V 3A TO-263) →
*Steps up battery voltage to 5V*

8. Insulation / Heat-shrink tubing & tape →
*For final wire management*

### -- Wiring & Resistors --
   
9. Wiring & Connectors / Female Jumper wires →
*Used for breadboard/prototyping*

10. 220Ω Resistors (for LEDs) →
*Prevent overcurrent*

11. 10kΩ Resistors (for pull-ups) →
*Prevent overcurrent*  
 
### -- Mechanical & 3D Print Supplies --
  
12. Structural shell / 3D-Printed Hammer Body
    
13. Grip Material / Rubber grip tape or silicone wrap
    
14. Fasteners / M3 screws, standoffs
    
15. Foam or Vibration Dampening / For sensor cushioning
 
### -- Tools Required --
  
16. Circuit assembly / Soldering iron + solder
    
17. Debugging/testing / Multimeter
    
18. Fixing components inside hammer / Hot Glue Gun
    
19. Structural fabrication / 3D Printer
    
20. Wiring / Wire strippers or cutters
 
### -- Testing & Debugging Components --
  
21. Arduino Programming / USB to Serial cable
    
22. Prototyping before permanent soldering / Cheap Breadboard
    
23. (Optional)If interfacing 3.3V or 5V devices / Logic Level shifter
    
24. Arduino IDE or PlatformIO serial debug / Serial monitor software

## Assembly Instructions on how to Complete The Rest of Project
1. Organize the hardware components you will use for the entire process
   
### -- Tools & Software --

2. Acquire the following tools:
   - Soldering iron * solder
   - Small screwdriver set
   - wire cutters
   - pliers
3. Download the following programs:
   - **KiCad:** circuit schematic & wiring design
   - **Fusion 360:** hammer casing 3D model
   - **Arduino IDE / PlatformIO:** firmware upload
   - **3D printer:** fabrication of hammer casing

### -- Overview of System Connections --
  
4. <ins>Recognize the Power Flow:</ins>

   Battery (3.7V) → Charger Module → Boost Converter → 5V line → Arduino Nano
   
5. <ins>Recognize the Signal Flow:</ins>

   LSM6DSV32XTR (I2C: SDA, SCL) → Arduino Nano
   
   Arduino Nano → Piezo Buzzer (Digital Pin)
   
   Arduino Nano → RGB LEDs (Digital Pin w/ 220Ω resistor)

### -- KiCad Schematic Design --
  
6. Open KiCad and create a new project

7. Add components:
   - Arduino Nano symbol (from library)
   - LSM6DSV32XTR symbol (I2C sensor)
   - Piezo buzzer
   - LEDs (and resistors)
   - Li-Po battery + charger + boost converter symbols 
8. Wire connections as outlined in Sections 4–5
9. Label nets (SDA, SCL, 5V, GND, LED_DATA, BUZZER)
10. Generate ERC (Electrical Rules Check) report — fix any open pins
11. Export the file to PDF, this is the schematic

***This was the last step I personally completed. Past here were the steps to do in the future***

### -- Mechanical Assembly Steps --
  
12. Slice and print both hammer head and handle in your chosen material (PLA for simplicity, PETG for strength)

13. Use reinforced infill (≥ 50%) for the head to handle impacts

14. Ensure the interior cavity dimensions fit the Arduino Nano and wiring harness

15. Test-fit parts before final assembly

16. Drill or design holes for:
   - USB port (for charging/programming)
   - LED windows on the hammer head
   - Small sound outlet for the piezo buzzer
17. Sand edges smooth for safety

### -- Electrical Assembly Steps --
  
18. Mount the Li-Po battery inside the handle cavity.

19. Connect the battery leads to the Linear Charger input (BAT+ / BAT–)

20. Wire the charger’s output to the Boost Converter’s input (3.7V IN)

21. Wire the Boost Converter output (5V OUT) to the Arduino Nano 5V pin

22. Common all grounds (battery, converter, sensor, Arduino)

23. Connect the Motion Sensor (LSM6DSV32XTR)
    <ins>GUIDE: (Sensor Pin / Arduino Nano Pin)</ins>
    - VCC / 3.3V ← *The sensor operates at 3.3V*
    - GND / GND ← *Common ground*
    - SDA / A4 ← *I2C data line*
    - SCL / A5 ← *I2C clock line*
    - INT1 / Optional (D2) ← *Interrupt for impact detection*

***Include 10 kΩ pull-up resistors on SDA/SCL lines to 3.3V if stability issues occur***

24. Connect the LEDs & Resistors
    <ins>GUIDE: (LED Type → Connection)</ins>
    - RGB LED (Common Anode or WS2812) → Connect data line to Arduino D6
    - Resistor (220 Ω) → Between Arduino pin and LED input
    - VCC → 5V from Boost Converter
    - GND → Common ground

***Test using the Adafruit_NeoPixel example sketch to confirm functionality***

25. Connect the Piezo Buzzer
    - Possitive side → D8 _(Digital Output for sound)_
    - Negative side → GND _Commond ground_

### -- Breadboard Testing --

26. Assemble all components on a full-size breadboard before soldering

27. Upload test firmware to verify:
    - Sensor reads acceleration
    - LEDs light correctly
    - Buzzer responds to motion
    - Power circuit holds stable at 5V

### -- Final Integration --
  
28. Transfer electronics from breadboard to perfboard or custom PCB (optional)

29. Secure components in the 3D-printed housing with screws or hot glue

30. Route wires neatly through the handle, use heat-shrink tubing for protection

31. Insert the USB charging port so it’s accessible from outside

32. Snap or screw the hammer head and handle together

### -- Firmware Installation --
  
33. Connect Arduino Nano via USB

34. Open firmware/main.ino in Arduino IDE

35. Select Board: Arduino Nano Every

36. Select Port: COMx

37. Upload firmware

38. Test by tapping the hammer head

39. Confirm that the LED lights + sound output occurs upon tapping the hammer

40. Take these extra steps for safety:
    - Do not charge while using the device.
    - Avoid over-discharging the Li-Po battery.
    - Store in a cool, dry environment.
    - Periodically check solder joints after repeated impacts.





