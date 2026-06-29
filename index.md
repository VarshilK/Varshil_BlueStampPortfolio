# SpaceCraft Motion Simulator
My project presents a way to control the motion of a spacecraft using servo motors. Currently, spacecrafts get thrown into the ocean after their use. By using the solution presented in this project, it is possible to actually land the spacecrafts on the ground to save time and money that is lost when retrieving a spacecraft from sea.

<!--You should comment out all portions of your portfolio that you have not completed yet, as well as any instructions:
```HTML 
<!--- This is an HTML comment in Markdown -->
<!--- Anything between these symbols will not render on the published site-->

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Varshil K | Emerald High School | Mechanical Engineering | Incoming Sophomore


<img width="480" height="641" alt="Varshil Headshot" src="https://github.com/user-attachments/assets/c25ed428-e130-4c80-8bd8-811416cc495d" />
  
<!--# Final Milestone

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
- What needs to be completed before your final milestone -->

# First Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/MNj89RGkUpo?si=f9XJmlA5Ue6vDcmE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

My Project is the SpaceCraft Motion Simulator, and this is my plan to complete my project:
- The components of my project so far include a full PCV Pipe Frame, 6 servo motors, 6 buttons, jumper wires and a large breadboard
- The progress I've made in my project so far includes getting all 3 servo motors to move freely back and forth using the 6 buttons attatched on the breadboard
- Some challenges I'm facing so far is problems with the servos moving too slow, or not moving smoothly. I plan to fix this by posssibly increasing the power input of the servos to increase their speed and improve the project.
- To complete my project, I hope to attatch all the CAD parts including the servo mount, servo dowel and rocket to it, and use the string to move the rocket around the frame.

# Starter Project

<iframe width="560" height="315" src="https://www.youtube.com/embed/GjduWvpThFo?si=GGB-SvRKq7--q_Zt" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

My starter project is a RetroArcade Game Console that uses soldering to hold the parts in place and complete the circuit. 
   - Some challenges I faced when building this project where that the solder would often touch between 2 different parts, which causes a short circuit, which can damage the batteries and parts in the project.
   - I enjoyed learning how to solder, and gained knowledge on electric components and how to transfer the current between the board and other components of the project
  
# Schematics

First Milestone Wiring:

<img width="705" height="658" alt="Wiring Diagram" src="https://github.com/user-attachments/assets/daee934d-0a04-43b9-a05c-613d282a8185" />

# Code

```c++
#include <Servo.h>;

const int servo1pin = 8;
const int servo2pin = 9;
const int servo3pin = 10;

const int button1 = 2;
const int button2 = 3;
const int button3 = 4;
const int button4 = 5;
const int button5 = 6;
const int button6 = 7;

int servo1forward; 
int servo1backward; 
int servo2forward;  
int servo2backward; 
int servo3forward;  
int servo3backward; 

const int stopspeed = 90;
const int forwardspeed = 180;
const int backwardspeed = 0;

Servo servo1;
Servo servo2;
Servo servo3;

void setup(){ 

  servo1.attach(servo1pin);
  servo2.attach(servo2pin);
  servo3.attach(servo3pin);

  pinMode(button1,INPUT_PULLUP);
  pinMode(button2,INPUT_PULLUP);
  pinMode(button3,INPUT_PULLUP);
  pinMode(button4,INPUT_PULLUP);
  pinMode(button5,INPUT_PULLUP);
  pinMode(button6,INPUT_PULLUP);

  Serial.begin(9600);
}

void loop(){ 
  servo1forward = !digitalRead(button1);
  servo1backward = !digitalRead(button2);
  servo2forward = !digitalRead(button3);
  servo2backward = !digitalRead(button4);
  servo3forward = !digitalRead(button5);
  servo3backward = !digitalRead(button6);
  
  // motor 1
  if(servo1forward && !servo1backward){ 
    servo1.write(forwardspeed);        
    Serial.print("Motor 1: Forward  | ");
  }
  else if(!servo1forward && servo1backward){
    servo1.write(backwardspeed); 
    Serial.print("Motor 1: Backward | ");
  }
  else{ 
    servo1.write(stopspeed);  
    Serial.print("Motor 1: Stopped  | ");
  }
  
  // motor 2
  if(servo2forward && !servo2backward){
    servo2.write(forwardspeed); 
    Serial.print("Motor 2: Forward  | ");
  }
  else if(!servo2forward && servo2backward){ 
    servo2.write(backwardspeed);           
    Serial.print("Motor 2: Backward | ");
  }
  else{ 
    servo2.write(stopspeed);  
    Serial.print("Motor 2: Stopped  | ");
  }
 
  if(servo3forward && !servo3backward){
    servo3.write(forwardspeed);  
    Serial.println("Motor 3: Forward  | ");
  }
  else if(!servo3forward && servo3backward){
    servo3.write(backwardspeed);   
    Serial.println("Motor 3: Backward | ");
  }
  else{
    servo3.write(stopspeed);  
    Serial.println("Motor 3: Stopped  | ");
  }

}
```

# Bill of Materials

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Arduino Uno R3 | Acts as the brain of the project, where I upload the code. Controls all the actions and movements of parts | $20.70 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| 3 Servo Motors | Spins the string, allows the spacecraft to move | $22.50 | <a href="https://www.elexp.com/products/29fs90rservo-continuous-rot?srsltid=AfmBOoodm4al84LFHUeoMycXLMbNuU7vi1NdhtlO_TPh-rBaxuLcOGDx"> Link </a> |
| Breadboard | Use to hold the wires in place without the need of soldering, allowing the electrical circuits to flow | $5.95 | <a href="https://lighthouseleds.com/full-size-solderless-breadboard-830.html?gad_source=4&gad_campaignid=17178518397&gbraid=0AAAAAChfWI3NjhuZVq8eWMCtTvGdKkh43&gclid=Cj0KCQjwo_PRBhDNARIsAEcVALX8ge15hzgJf0yn9wduaXPoXm3wAcBml5cnGxUWID2pONDeZ1opB8UaAoBJEALw_wcB"> Link </a> |

<!--# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.-->
