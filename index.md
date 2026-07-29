# Arduino Robotic Arm
This project is an Arduino-controlled robotic arm designed to perform several basic arm movements through a custom joystick controller. Four motors control the system: two move the arm’s joints, one rotates the base, and one opens and closes the gripper. The Arduino board receives input from a homemade controller with two joysticks, allowing the arm to move in multiple directions.

You should comment out all portions of your portfolio that you have not completed yet, as well as any instructions:
```HTML 
<!--- This is an HTML comment in Markdown -->
<!--- Anything between these symbols will not render on the published site -->
```

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Jerry Xiang | Portola High | Electrical Engineering | 11th

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
# Final Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your final milestone, explain the outcome of your project. Key details to include are:
- What you've accomplished since your previous milestone
- What your biggest challenges and triumphs were at BSE
- A summary of key topics you learned about
- What you hope to learn in the future after everything you've learned at BSE



# Second Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/y3VAmNlER5Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your second milestone, explain what you've worked on since your previous milestone. You can highlight:
- Technical details of what you've accomplished and how they contribute to the final goal
- What has been surprising about the project so far
- Previous challenges you faced that you overcame
- What needs to be completed before your final milestone 

# First Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/vh_s0m1IfjQ" title="First Milestone Video: Robotic Arm Assembly" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

The project is an Arduino-controlled robotic arm that has been fully assembled and connected to its main circuit. It uses four servo motors: two control the arm joints, one rotates the base, and one opens and closes the gripper. A custom controller with two analog joysticks will provide input for these movements.

This milestone video presents the completed physical structure of the robotic arm and explains how the arm will move after programming. The small screws made assembly difficult because they were hard to hold in place, so a magnetic screwdriver was used to keep them attached to the screwdriver during installation.

The next step is to program and test the control system. The completed project will support direct manual control through the joysticks and a preset automatic routine that moves lightweight objects between two fixed locations.

# Schematics 
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. 

# Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

```c++
void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
  Serial.println("Hello World!");
}

void loop() {
  // put your main code here, to run repeatedly:

}
```

# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| 1 MG90S servo | Drive the base | $5 | <a href="https://www.pishop.us/product/mg90s-micro-servo-metal-gear/"> Link </a> |
| 3 SG90 servo | Drive the robotic arm | $Price | <a href="https://www.amazon.com/AILUOMI-Micro-Compatible-Arduino-Raspberry/dp/B0G4W4X1H9/ref=sr_1_3?crid=2U7CJFDKN8D5Y&dib=eyJ2IjoiMSJ9.CTzwxdFnBiabc1f6Sr4-oNBaOr_JUXNPRiwmRLsQzgM9eKt7OxGLjeVWd6C6PLbj8L-9ns4AzKjWEwetsdtPr_c6VFSvlh-KEqixO_n82jVvoMZHV55FtN8PG6XQ_FpQQvD5OrDG41-2ixtWP5rFAIXU8_glfgHFkzU0ZQCv4_64-WT1qVkFbCTvzCMmKlrmi8D__CidRkyGjWr8-trYriBRBDwQT0MFw0p7poScHSLBljUEJ4wBwZXzXk8iWCRmw9tIzruQAdfc8RhzCIoTZ9_0JsJ3IKasvC34E469Ld8.lXiu7l-BFjcLor_8p_zC4q2Rp6Fg4T_Dxz2SlaLf0pI&dib_tag=se&keywords=one+SG90&qid=1785336540&s=toys-and-games&sprefix=one+sg90%2Ctoys-and-games%2C155&sr=1-3"> Link </a> |
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |

# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
