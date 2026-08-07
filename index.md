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
