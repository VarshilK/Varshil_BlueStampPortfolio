# Altitude Control Test Rig
My project models how a spacecraft can change its position and orientation in space using continuous and smooth motion inputs. Modern day spacecrafts use on and off thrusters for their motion, making tiny adjustments extremely difficult. Engineers are currently attempting to solve this issue, which is why I build this project to look into it myself.

<!--You should comment out all portions of your portfolio that you have not completed yet, as well as any instructions:
```HTML 
<!--- This is an HTML comment in Markdown -->
<!--- Anything between these symbols will not render on the published site-->

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Varshil K | Emerald High School | Robotics Engineering | Incoming Sophomore


<img width="480" height="641" alt="Varshil Headshot" src="https://github.com/user-attachments/assets/c25ed428-e130-4c80-8bd8-811416cc495d" />
</>
<img width="255" height="205" alt="Screenshot 2026-07-30 at 9 54 52 PM" src="https://github.com/user-attachments/assets/1786019e-ef59-46ae-9a8e-be003fa994ed" />
<img width="557" height="481" alt="Screenshot 2026-07-30 at 9 55 14 PM" src="https://github.com/user-attachments/assets/a6daf99e-7f04-45d5-a496-41d393fcfbb2" />


  
# Final Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For my final milestone, I completed all of my modifications, and created a neat final project:
- I added a fourth servo motor to control the pitch of the space shuttle to ensure every single movement was fully controlled. I added a bluetooth connection between HC-05 modules between a video game controller that I cadded and printed and my project frame. I cadded four frame base parts that could connect with each other and hold the major electrical components of my frame including an arduino uno r3, HC-05, battery, and breadboard.
- The biggest challenge I faced with my modifications were with the bluetooth connection, with frequent jittering of my servo motors. I solved this issue with creative code techniques, such as only sending the joystick values from the arduino nano and arduino when there was a notable change in the joystick position. As I continued these creative code techniques, I narrowed down the issues, and made sure there was no jittering at all in the end.
- With these modifications, I refined my CAD skills, learned advanced breadboard electronics, the use of microcontrollers, transferring information between microcontrollers, and many more that I will carry on with me in the future.
- In the future, I hope to add an IMU (Inertial Movement Unit) to my project, which will allow me to track the location, orientation, needed thrust, needed fuel, and many more details of the spacecraft to use in a real spacecraft launch.



# Second Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/RI52WIFWxVE?si=bzAFpatfKlo8aq7J" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

For my second milestone, I finished building my entire base project, and expanded on my first milestone:
- I printed 3 servo dowels, attached each of them onto my servo arms, added string to them, and finally attached my 3-d printed space shuttle onto it
- The challenges that I overcame in my project were that the string would often come off of the servo dowel, which is why I changed the position of my servo mount so that the string would always stay on the dowel
- Before my final milestone, I need to add in a fourth servo motor, and get my space shuttle controlled fully by joysticks instead of arduino buttons


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

# Arduino Uno Code

```c++
#include <SoftwareSerial.h>
#include <Servo.h>

SoftwareSerial BTSerial(10, 11); // RX, TX

Servo servo1, servo2, servo3, servo4;
const int servoPins[4] = {7, 8, 2, 4};

String inputBuffer = "";
bool receiving = false;

int lastAngles[4] = {90, 90, 90, 90};
const int DEADZONE = 15;
const int CENTER_ZONE = 8;

bool reversed[4] = {
  true,
  false,
  true,
  false,
};

const int BUTTON_SPEED_OFFSET = 50;

void setup() {
  Serial.begin(9600);
  BTSerial.begin(9600);

  servo1.attach(servoPins[0]);
  servo2.attach(servoPins[1]);
  servo3.attach(servoPins[2]);
  servo4.attach(servoPins[3]);

  servo1.write(lastAngles[0]);
  servo2.write(lastAngles[1]);
  servo3.write(lastAngles[2]);
  servo4.write(lastAngles[3]);

  Serial.println("Uno (Slave) ready - driving servos");
}

void loop() {
  while (BTSerial.available()) {
    char c = BTSerial.read();

    if (c == '<') {
      inputBuffer = "";
      receiving = true;
    } else if (c == '>') {
      receiving = false;
      parseAndSetServos(inputBuffer);
    } else if (receiving) {
      inputBuffer += c;
    }
  }
}

void spinButton1() {
  servo1.write(90 + BUTTON_SPEED_OFFSET);
  servo3.write(90 + BUTTON_SPEED_OFFSET);
}

void spinButton2() {
  servo1.write(90 - BUTTON_SPEED_OFFSET);
  servo3.write(90 - BUTTON_SPEED_OFFSET);
}

void parseAndSetServos(String data) {
  int values[6];
  int idx = 0;
  int lastComma = -1;

  for (int i = 0; i < (int)data.length() && idx < 6; i++) {
    if (data[i] == ',' || i == (int)data.length() - 1) {
      int endIdx = (data[i] == ',') ? i : i + 1;
      String piece = data.substring(lastComma + 1, endIdx);
      values[idx] = piece.toInt();
      idx++;
      lastComma = i;
    }
  }

  if (idx != 6) return;

  bool buttonPressed = (values[4] == 1);
  bool button2Pressed = (values[5] == 1);

  int newAngles[4];
  newAngles[0] = map(values[0], 0, 1023, 0, 180);
  newAngles[1] = map(values[1], 0, 1023, 0, 180);
  newAngles[2] = map(values[2], 0, 1023, 0, 180);
  newAngles[3] = map(values[3], 0, 1023, 0, 180);

  for (int i = 0; i < 4; i++) {
    if (reversed[i]) {
      newAngles[i] = 180 - newAngles[i];
    }
  }

  if (buttonPressed) {
    spinButton1();
  } else if (button2Pressed) {
    spinButton2();
  } else {
    if (abs(newAngles[0] - 90) <= CENTER_ZONE) {
      servo1.write(90);
      lastAngles[0] = 90;
    } else if (abs(newAngles[0] - lastAngles[0]) >= DEADZONE) {
      servo1.write(newAngles[0]);
      lastAngles[0] = newAngles[0];
    }

    if (abs(newAngles[2] - 90) <= CENTER_ZONE) {
      servo3.write(90);
      lastAngles[2] = 90;
    } else if (abs(newAngles[2] - lastAngles[2]) >= DEADZONE) {
      servo3.write(newAngles[2]);
      lastAngles[2] = newAngles[2];
    }
  }

  // servo2 and servo4 always joystick-controlled, unaffected by either button
  if (abs(newAngles[1] - 90) <= CENTER_ZONE) {
    servo2.write(90);
    lastAngles[1] = 90;
  } else if (abs(newAngles[1] - lastAngles[1]) >= DEADZONE) {
    servo2.write(newAngles[1]);
    lastAngles[1] = newAngles[1];
  }

  if (abs(newAngles[3] - 90) <= CENTER_ZONE) {
    servo4.write(90);
    lastAngles[3] = 90;
  } else if (abs(newAngles[3] - lastAngles[3]) >= DEADZONE) {
    servo4.write(newAngles[3]);
    lastAngles[3] = newAngles[3];
  }
}
```
# Arduino Nano Code

```c++
#include <SoftwareSerial.h>

SoftwareSerial BTSerial(2, 3); // RX, TX

const int joyPins[4] = {A0, A1, A2, A3};
const int buttonPin = A4;
const int buttonPin3 = A5; // physically button3, fills the "button2" slot in the packet

int centerValues[4];
int lastSentValues[4];

const int MOVE_THRESHOLD = 100;

void setup() {
  Serial.begin(9600);
  BTSerial.begin(9600);
  pinMode(buttonPin, INPUT_PULLUP);
  pinMode(buttonPin3, INPUT_PULLUP);
  Serial.println("Nano (Master) calibrating joystick centers...");

  delay(1000);

  for (int i = 0; i < 4; i++) {
    long sum = 0;
    for (int j = 0; j < 20; j++) {
      sum += analogRead(joyPins[i]);
      delay(5);
    }
    centerValues[i] = sum / 20;
    lastSentValues[i] = 512;

    Serial.print("Joystick ");
    Serial.print(i);
    Serial.print(" center: ");
    Serial.println(centerValues[i]);
  }

  Serial.println("Calibration done. Reading joysticks...");
}

void loop() {
  int values[4];
  bool anyChanged = false;

  for (int i = 0; i < 4; i++) {
    long sum = 0;
    for (int j = 0; j < 5; j++) {
      sum += analogRead(joyPins[i]);
      delayMicroseconds(50);
    }
    int raw = sum / 5;

    int adjusted = raw - centerValues[i] + 512;
    if (adjusted < 0) adjusted = 0;
    if (adjusted > 1023) adjusted = 1023;

    if (abs(adjusted - lastSentValues[i]) >= MOVE_THRESHOLD) {
      values[i] = adjusted;
      lastSentValues[i] = adjusted;
      anyChanged = true;
    } else {
      values[i] = lastSentValues[i];
    }
  }

  bool buttonPressed = (digitalRead(buttonPin) == LOW);
  bool button3Pressed = (digitalRead(buttonPin3) == LOW);

  if (anyChanged || buttonPressed || button3Pressed) {
    BTSerial.print('<');
    for (int i = 0; i < 4; i++) {
      BTSerial.print(values[i]);
      BTSerial.print(',');
    }
    BTSerial.print(buttonPressed ? 1 : 0);
    BTSerial.print(',');
    BTSerial.print(button3Pressed ? 1 : 0);
    BTSerial.print('>');
  }

  delay(200);
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

# Other Resources
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
