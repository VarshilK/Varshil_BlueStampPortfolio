# SpaceCraft Motion Simulator
My project presents a way to control the motion of a spacecraft using servo motors. Currently, spacecrafts get thrown into the ocean after their use. By using the solution presented in this project, it is possible to actually land the spacecrafts on the ground to save time and money that is lost when retrieving a spacecraft from sea.

<!--You should comment out all portions of your portfolio that you have not completed yet, as well as any instructions:
```HTML 
<!--- This is an HTML comment in Markdown -->
<!--- Anything between these symbols will not render on the published site-->

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Varshil K | Emerald High School | Robotics Engineering | Incoming Sophomore


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

First Milestone Circuit Diagram:


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
| RetroArcade Game Console | Starter Project kit that uses soldering to simulate a small video game console | $17.99 | <a href="https://www.amazon.com/Electronic-Soldering-Practice-Comfortable-VOGURTIME/dp/B094QRRHC2/ref=sr_1_2_sspa?crid=3ANJQTEW8NNXF&dib=eyJ2IjoiMSJ9.i380idwTPEs8eXFg2laDxtcMQ88I2s6LbjHr8wPJV77pwdSkdDmxCBVNCK3DDJj_oNm_Htj8iQ8ELuq4vXGikeC4xEHmpLRiBwInY73jCLA.tcv87PyRRjVPSjKTeLGGn8V-yhCm4CLF_rZEvziEVgY&dib_tag=se&keywords=arcade%2Bsolder%2Bkit&qid=1746029304&s=electronic&th=1"> Link </a> |
| Arduino Uno R3 | Acts as the brain of the project, where I upload the code. Controls all the actions and movements of parts | $20.70 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/?th=1"> Link </a> |
| 3 Continuous Rotation Servo Motors | Spins the string, allows the spacecraft to move | $11.70 | <a href="https://www.dfrobot.com/product-1579.html?gad_source=1&gad_campaignid=23441887437&gbraid=0AAAAADucPlD34auuX1xtNqduI7G2AiraN&gclid=CjwKCAjwuanRBhBSEiwAY5y6V7RrTcx7V8Lqe1Ma7bmWSV0-BceUJpX8WVjEneTKtP1owQD_co-dQBoCcWIQAvD_BwE"> Link </a> |
| Large Breadboard | Use to hold the wires in place without the need of soldering, allowing the electrical circuits to flow | $6.99 | <a href="https://www.amazon.com/SHILLEHTEK-Breadboard-Raspberry-Microcontrollers-Connectors/dp/B0CW231CR4/ref=sr_1_21?crid=24SMKTNE2QQ44&dib=eyJ2IjoiMSJ9.IEnHb8CCHQhBJ7Niz_wqqx2hCNaZzyCXV93W7bRFSK5k9G0cGk3KImPkhCGxzT6lwPe4IldcnNNUtRmwSJbhGaZlcL2Bycn8btOVgAd6mF8CNmU7msnHBipnF6ogA1MaWkTGMqZg2t0x47zCi7L2wHmHFsebtTUcHkdwlqWxR-TF6jVZMc3O6W7LZdy4yQI786-QxTeJrSNd2-wImhCDOgSQE2DXX2ckyEuSnonevkzuQpIQFg7Oq51s7IYHzWcBmDJAwbwxdB9wmzZEVbx2Rru8vIX1pfRRRpM9l569yoI.qKyZOdAWMcTkfTWe_TieTdmEu6zW5yquwP-frefjeQM&dib_tag=se&keywords=1%2Blarge%2Bbreadboard&qid=1783026015&s=electronics&sprefix=%2Celectronics%2C265&sr=1-21&th=1"> Link </a> |
| 8 PVC Elbow Connectors| These are used to connect the PVC pipes and keep the frame held together | $5.44 | <a href="https://www.amazon.com/20-Pack-Fittings-Furniture-Connector-Structure/dp/B0DCBB8JXG/ref=sr_1_1_sspa?dib=eyJ2IjoiMSJ9.00Vvh4WQl08k4jKimsiQJuvwNQbCDS5YLg2wmozY3jTrlF92ql8Y4yk5zjf6ycZiqAXSoyTqFUQ9zDT8kWXujnV5cChFjRrK4KMi_EdSDb7QEU3_jYuxEEgf7qIDNiUz7vCNP8zkN9oO-5iy37LXjDoJaqYoEbh6K6ZRPd8cfehcuTZiHxQGOUIVQRecQkYynfWmpyrzbfIQNGYyZBDrzJhNRcb09A83UAUtFItOFGQ.qPP3Nsv7s6wvWtyoYU5basLknJr1pCp9tXzy6TENnYA&dib_tag=se&keywords=3%2Bway%2Bpvc%2Belbow&qid=1781195169&sr=8-1-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&th=1"> Link </a> |
| PVC Pipes | Acts as the frame of the project, where the servos are attatched to and where the rockets moves in | $28.80 | <a href="https://www.amazon.com/CKVIHAV-Industrial-Greenhouse-Workshop-Furniture/dp/B0DWSFXG31/ref=sr_1_5?crid=35A09K66FQNM4&dib=eyJ2IjoiMSJ9.XG0mf-BDPSCk-5yI77dMLMs3ddTK1iigyuSsf_3x5xow_CcMTocJH5XCbxgW0lxfDaPHrB3LWI0Gvd0LK5uRXatxGvVlpY6nvcOHwgv0PZ-Bgwc9R2AelknO86prrRx_G1-l91qxO9xS1MHiZ4N9_QAJ615mG4T0hsRfmwqhSfxHItXt6lWoax0C-SK6UPhJmQBM7YPNMGrg-lurVq39O3YDgY05Fg4cLJ_f17p6MGA.mZiygtu0KSnkVJ7SKbMw5CSyqkpxbJnF7r_e7oDZdCI&dib_tag=se&keywords=1%2F2%22%2Bdiameter%2BPVC%2Bpipe%2B-%2B12%2Bft&qid=1783025433&sprefix=3%2Bway%2Bpvc%2Belbow%2Caps%2C381&sr=8-5&th=1"> Link </a> |
| Male to Male jumper wires | Allow the electrical current to flow between all of the components on the breadboard | $1.95 | <a href="https://www.digikey.com/en/products/detail/adafruit-industries-llc/1956/6827089?gclsrc=aw.ds&gad_source=1&gad_campaignid=20232005509&gbraid=0AAAAADrbLlj-PNzwtHkhzqoeioBvJGE9q&gclid=CjwKCAjwmJjSBhB-EiwAkZgxi531cXU62YreEUSlOpMSG4wYAbvVWWK82r3o1hCphhPJLd2j3SFWHxoCevsQAvD_BwE"> Link </a> |
| 6 Breadboard Buttons | Connect to the breadboard and are used to move the servos back and forth | $2.93 | <a href="https://www.digikey.com/en/products/detail/sparkfun-electronics/14460/7915747?gclsrc=aw.ds&gad_source=1&gad_campaignid=20243136172&gbraid=0AAAAADrbLlj1fOpVS-J9OCclJDTSNeTLj&gclid=CjwKCAjwuanRBhBSEiwAY5y6V8mlnmJvqqdaVgelS-AyD3Dh3BkGUHFYLTWQ_g0l-Bhclth4FxT3rhoCd3kQAvD_BwE"> Link </a> |
| String | Connected to the servo motors and move the space shuttle around the frame | $4.59 | <a href="https://www.amazon.com/Cotton-Bakers-String-Wrapping-Packaging/dp/B07KW42VDC/ref=sr_1_2_sspa?dib=eyJ2IjoiMSJ9.CdgXAo0yEAB0jCxAr3DoObF_G1NJdNgW8gsejlAzd72nPp9eTa4PDHorXZmGG7WrbT8Qw3wbNUEIW9WoBV9bRAYzpvU0lKfmsskeWX4cDKF7nbj8FPfmFGo00C8CtCHQLF5lT6WUlcY0UlhqLY-vJv4ODwAwfCBq6furAjFhbpohm4fv06kQnQ0pDCScdAZmCf94Al7YmAsbyBpgfm_I5vDC5GW-KDS5Z26JENLZzVXDTraJYhMDeh_JdaRquM8-dgtdJueTNvpdg0CDpgHjiUrsaH7yqzi6AljlMLVLR8w.KRLVnKHTfFNi7KKpJabTNHn6JwO_x2OPAQXLu3QnwXw&dib_tag=se&keywords=string&qid=1781195080&sr=8-2-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&th=1"> Link </a> |

<!--# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.-->
