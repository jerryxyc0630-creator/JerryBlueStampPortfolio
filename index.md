# Arduino Robotic Arm

This Arduino-controlled robotic arm uses four servo motors: two move the main arm joints, one rotates the base, and one opens and closes the claw. It is controlled by a custom handheld controller with two joysticks and a separate breadboard control board with three buttons and three LEDs. The system supports two manual-control modes as well as a short record-and-playback function.

| **Engineer** | **School** | **Area of Interest** | **Grade** |
| :----------: | :--------: | :------------------: | :-------: |
| Jerry Xiang | Portola High | Electrical Engineering | 11th |

<!--
## Project Photo

Add a photo of Jerry and the completed robotic arm here after uploading the image file to this branch.

![Completed Arduino robotic arm](project-photo.jpg)
-->

# First Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/vh_s0m1IfjQ" title="First Milestone Video: Robotic Arm Assembly" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

At this milestone, the physical structure of the robotic arm had been fully assembled and connected to its main circuit. The arm uses four servo motors: two control the arm joints, one rotates the base, and one opens and closes the claw. A custom controller with two analog joysticks provides input for these movements.

This video presents the completed physical structure of the robotic arm and explains how the arm will move after programming. The small screws made assembly difficult because they were hard to hold in place, so a magnetic screwdriver was used to keep them attached during installation.

The next step was to program and test the control system, including direct joystick control and a record-and-playback routine.

# Second Milestone

<!--
Add the Second Milestone YouTube embed here after the video is uploaded.

<iframe width="560" height="315" src="https://www.youtube.com/embed/VIDEO_ID" title="Second Milestone Video" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
-->

<iframe width="560" height="315" src="https://www.youtube.com/embed/cyYA59lS46Y" title="Second Milestone Video: Original Robotic Arm Control System" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

Since the first milestone, the robotic arm has been programmed and tested using the original Cokoino control system. The system uses a custom handheld controller with two joysticks and four servo motors. One servo rotates the base, two servos move the main arm joints together, and the final servo opens and closes the claw.

In the original control layout, one joystick controls the coordinated movement of the two arm joints and the rotation of the base. The other joystick controls the claw and the original recording functions. The program can save up to ten arm positions and replay them in sequence.

The main challenge was servo calibration. At first, the physical arm parts were not aligned with the servos’ programmed starting angles, causing the arm to move into incorrect positions when powered on. Each servo was centered, the servo horns were reinstalled, and the mechanical parts were aligned so that the arm could start and move safely.

This milestone focuses on completing and testing the original robotic arm system. At this stage, there was no added breadboard control board, extra buttons, LEDs, or custom control modes.

# Final Milestone

<!-- Add the Final Milestone YouTube embed here after the video is uploaded. -->

Since the second milestone, the original robotic-arm control system has been upgraded with a custom breadboard control board. The completed system uses three buttons and three LEDs in addition to the two-joystick handheld controller. The four servo motors control the base, lower arm joint, upper arm joint, and claw.

Two operating modes were added. In Mode 1, each joystick axis controls a separate part of the arm, allowing more precise movement of the base, lower joint, upper joint, and claw. In Mode 2, one joystick controls the two main arm joints together, making it easier to extend or retract the arm. When Mode 2 is selected, the two arm joints return to their calibrated starting positions. The mode LED is on in Mode 1 and off in Mode 2.

A recording and playback system was also added. Pressing the record button starts saving the positions of all four servos every 0.25 seconds. The recording LED flashes during the first five seconds and flashes faster during the final five seconds. Recording is limited to ten seconds because the Arduino Nano has limited memory. Pressing the record button again saves the movement and keeps the LED on; pressing it one more time deletes the saved recording. The play button makes the arm repeat the saved sequence while the playback LED is on.

The largest challenge was servo calibration. The program can command each servo to move to a specific angle, but the physical servo horns and arm parts must also be installed at matching angles. Incorrect alignment initially caused the arm to move into unsafe positions when powered on. Centering the servos, reinstalling the servo horns, and realigning the mechanical parts solved this problem.

This project demonstrated how mechanical design, circuits, and programming work together in one system. Important topics included reading analog joystick input, controlling servo angles, using digital buttons and LEDs, managing limited Arduino memory, and debugging a physical system.

In the future, the system could be expanded to store longer recordings and multiple separate actions. A number display could show the selected action, allowing the user to choose and replay different saved routines.

# Schematics

[View the complete robotic-arm wiring schematic (PDF)](Epic%20Blad.pdf)

# Wiring Summary

| **Component** | **Arduino Pin(s)** | **Purpose** |
| :----------- | :---------------- | :---------- |
| Base servo | D4 | Rotates the base |
| Lower arm servo | D5 | Moves the lower arm joint |
| Upper arm servo | D6 | Moves the upper arm joint |
| Claw servo | D7 | Opens and closes the claw |
| Mode button | D8 | Switches between Mode 1 and Mode 2 |
| Record button | D9 | Starts, saves, and deletes a recording |
| Play button | D10 | Replays the saved movement |
| Mode LED | D11 | On for Mode 1; off for Mode 2 |
| Recording LED | D12 | Shows recording and saved-recording status |
| Playback LED | D13 | Turns on during playback |
| Two joystick modules | A0–A3 | Sends four analog control signals |

<!--
Add a wiring-diagram image here after exporting and uploading it to this branch.
-->

# Code

The Arduino program uses the CokoinoArm library to read joystick input, control the four servos, switch between operating modes, and store a short sequence of servo positions for playback.

```c++
#include "src/CokoinoArm.h"

CokoinoArm arm;

const byte MODE_BUTTON_PIN   = 8;
const byte RECORD_BUTTON_PIN = 9;
const byte PLAY_BUTTON_PIN   = 10;

const byte MODE_LED_PIN   = 11;
const byte RECORD_LED_PIN = 12;
const byte PLAY_LED_PIN   = 13;

const unsigned long RECORD_LIMIT_MS = 10000UL;
const unsigned long SAMPLE_INTERVAL = 250UL;
const byte MAX_FRAMES = 40;

void setup() {
  // D4 base, D5 lower joint, D6 upper joint, D7 claw
  arm.ServoAttach(4, 5, 6, 7);

  // Two joystick modules
  arm.JoyStickAttach(A1, A0, A3, A2);

  pinMode(MODE_BUTTON_PIN, INPUT_PULLUP);
  pinMode(RECORD_BUTTON_PIN, INPUT_PULLUP);
  pinMode(PLAY_BUTTON_PIN, INPUT_PULLUP);

  pinMode(MODE_LED_PIN, OUTPUT);
  pinMode(RECORD_LED_PIN, OUTPUT);
  pinMode(PLAY_LED_PIN, OUTPUT);
}

void loop() {
  // Read joystick input.
  // Control the arm in Mode 1 or Mode 2.
  // Check the mode, record, and playback buttons.
  // Save up to 40 servo-position frames for a maximum of 10 seconds.
}
```

# Bill of Materials

| **Part** | **Quantity** | **Price** | **Link** |
| :------- | :----------: | :-------: | :------- |
| Robot Arm Kit | 1 | $45.00 | [Link](https://www.amazon.com/LK-COKOINO-Compliment-Engineering-Technology/dp/B081FG1JQ1) |
| Servo Shield / Nano Sensor Shield V5.0 | 1 | $2.95 | [Link](https://protosupplies.com/product/sensor-shield-v5-0/) |
| Magnetic Precision Screwdriver Kit | 1 | $4.75 | [Link](https://www.walmart.com/ip/Precision-Screwdriver-Set-25-in-1-Multi-Bit-Magnetic-Tool-Kit-Alloy-Steel-Bits-Non-Slip-Handle-Leather-Case-Mini-Portable-Repair-Glasses-Watches-Elec/19283665968) |
| Electronics Kit | 1 | $12.79 | [Link](https://www.walmart.com/ip/Electronic-Component-Wires-Breadboard-LED-Buzzer-Resistor-Transistor-Starter-Set/936088703) |
| 2 × 18650 Battery Holder with DC Barrel Plug | 1 | $13.78 | [Link](https://www.ebay.com/itm/406247835485) |
| Digital Multimeter (DMM) | 1 | $9.99 | [Link](https://www.walmart.com/c/kp/digital-multimeter) |
| 2 × 18650 Rechargeable Batteries | 1 set | $11.99 | [Link](https://www.ecogearfx.com/product/18650-rechargeable-lithium-ion-battery-2-pack/) |
| **Total** |  | **$101.25** |  |

# Other Resources

- [Cokoino CKK0006 robotic arm source code](https://github.com/Cokoino/CKK0006)
- [Arduino Nano documentation](https://docs.arduino.cc/hardware/nano/)
- [Arduino Servo library documentation](https://docs.arduino.cc/libraries/servo/)
- [BlueStamp Engineering portfolio template](https://github.com/BlueStampEng/BSE_Template_Portfolio)

<!--
# Final Milestone

This section will be added after the final presentation and video are complete.
-->
