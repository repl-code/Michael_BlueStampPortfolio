# Phone-Controlled Robotic Arm
The robotic arm is an amazing introduction to the world of robotics and engineering. I learned both important engineering skills and important coding skills to complete this project.<!-- You can include what the biggest challenges, takeaways, and triumphs from completing the project were. As you complete your portfolio, remember your audience is less familiar than you are with all that your project entails! -->



| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Michael T | Mission San Jose High School | Mechanical/Aerospace Engineering | Incoming Sophomore |



[headstone image](Michael_T(1).heic) 

<!---

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

# Third Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/XuP0vEEQgEo?si=vrGobZevF6jQSOZD" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

# Code for the Third Milestone
'''
'''

-->

# Second Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/6N0BU17_WHo?si=kGL2fw3Crfc0Hj9E" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

The second milestone was rocky and full of bugs. For this step, I coded the servo to be able to be controlled by the joysticks on the controller. The joystick gave x and y outputs of 0-1000, but sometimes the range varied from 0-500 or 0-700. My code would take the 4 joystick's default position's output and add a buffer of about 20 to make sure the servos did not move from a slight change of output. I also wired the DSD TECH HC-05 bluetooth module and connected to it to a test app I made in MIT app inventor. When I pressed the pin on button in the app, the phone would communicate with the Arduino on the serial monitor and configure the pin's output to high and make a buzzing sound with the buzzer. I had many, many challenges for this milestone. The code provided to control the arm with the joysticks did not work, even after spending many hours trying to debug it. I had several errors preventing the program from even starting, such as exit status 1 and my Arduino nano board not responding. I found out all of the servos broke too, probably from the program having the arm spin around and pulling the wires too hard. The servos went so haywire that part of the structure broke as well I had to superglue the structure and replace all of the servos. My code also had many bugs I had to work on, such as unoptimized code, malfunctioning joystick inputs, and the nonresponding servos. My code determining which direction the servos should move could not work as well, and I solved this by redoing the entire code step by step. I learned to make sure that the code works for one of the servos instead of trying to code for all four at once. I had many difficulties reaching this milestone, but I am glad I learned a lot from it.

# Code for Second Milestone 

```
/*Controller Code for 4-Joint Robotic Arm by Michael Tzeng */
#include <Servo.h> //servo library to control servos

Servo myservoone; //establishing servos
Servo myservotwo;
Servo myservothree;
Servo myservofour;

#define xLpin A1 //controller input pin
#define yLpin A0
#define xRpin A3
#define yRpin A2

int servoangleone = 90; //variable that is what the servo angle is programmed to be
int servoangletwo = 90;
int servoanglethree = 90;
int servoanglefour = 90;

int xL; //controller input
int xLchange = 0;
int xLd = analogRead(xLpin); //base position

int yL; //controller input
int yLchange = 0;
int yLd = analogRead(yLpin); //base position

int xR; //controller input
int xRchange = 0;
int xRd = analogRead(xRpin); //base position

int yR; //controller input
int yRchange = 0;
int yRd = analogRead(yRpin); //base position

int y = 50; 
int x = 0; 
int z = 0; //toggle servos on/off

int i1 = 10; //other variables
int i2 = 6;
int i3 = 5;
int i4 = 6;

void setchangeangle(){ //decides which way the servo should move based on controller input
  xL=analogRead(xLpin);
  if (xL >= xLd + y) {
    xLchange = 1;
  } else if (xL <= xLd - y) {
    xLchange = -1;
  } else {
    xLchange = 0;
  }

  yL=analogRead(yLpin);
  if (yL >= yLd + y) {
    yLchange = 1;
  } else if (yL <= yLd - y) {
    yLchange = -1;
  } else {
    yLchange = 0;
  }

  xR=analogRead(xRpin);
  if (xR >= xRd + y) {
    xRchange = 1;
  } else if (xR <= xRd - y) {
    xRchange = -1;
  } else {
    xRchange = 0;
  }

  yR=analogRead(yRpin);
  if (yR >= yRd + y) {
    yRchange = 1;
  } else if (yR <= yRd - y) {
    yRchange = -1;
  } else {
    yRchange = 0;
  }
}

void setservoangle(){ //using void setchangeangle(), this changes where you want the servo to be
  xLchange = xLchange * i1;
  yLchange = yLchange * i2;
  xRchange = xRchange * i3;
  yRchange = yRchange * i4;

  if (servoangleone + xLchange <= 175, servoangleone + xLchange >= 5) {
    servoangleone = servoangleone + xLchange;
  }

  if (servoangletwo + yLchange <= 175, servoangletwo + yLchange >= 5) {
    servoangletwo = servoangletwo + yLchange;
  }

  if (servoanglethree + xRchange <= 175, servoanglethree + xRchange >= 5) {
    servoanglethree = servoanglethree + xRchange;
  }

  if (servoanglefour + yRchange <= 95, servoanglefour + yRchange >= 5) {
    servoanglefour = servoanglefour + yRchange;
  }
} 

void capservoangle() { //its caps the servo angle so it is not told to go over 180 or under 0
  if (servoangleone >= 180){
    servoangleone = 180;
  }
  if (servoangleone <= 0) {
    servoangleone = 0;
  }

  if (servoangletwo >= 180){
    servoangletwo = 180;
  }
  if (servoangletwo <= 0) {
    servoangletwo = 0;
  }

  if (servoanglethree >= 180){
    servoanglethree = 180;
  }
  if (servoanglethree <= 0) {
    servoanglethree = 0;
  }

  if (servoanglefour >= 100){
    servoangleone = 100;
  }
  if (servoanglefour <= 0) {
    servoanglefour = 0;
  }
}

void servomove() {
  if (z=1) {
    if (servoangleone != myservoone.read()) {
      myservoone.write(servoangleone);
      delay(100);
    }

    if (servoangletwo != myservotwo.read()) {
      myservotwo.write(servoangletwo);
    }

    if (servoanglethree != myservothree.read()) {
      myservothree.write(servoanglethree);
    }

    if (servoanglefour != myservofour.read()) {
      myservofour.write(servoanglefour);
    }
  }
}

void print() {
  Serial.print("servo 1 = ");
  //Serial.println(myservoone.read());
  Serial.println(servoangleone);
  Serial.print("servo 2 = ");
  //Serial.println(myservotwo.read());
  Serial.println(servoangletwo);
  Serial.print("servo 3 = ");
  //Serial.println(myservothree.read());
  Serial.println(servoanglethree);
  Serial.print("servo 4 = ");
  //Serial.println(myservofour.read());
  Serial.println(servoanglefour);
}

void setup() { 
  Serial.begin(9600);
  xLd = analogRead(xLpin);
  yLd = analogRead(yLpin);
  xRd = analogRead(xRpin);
  yRd = analogRead(yRpin);
  myservoone.attach(6);
  myservotwo.attach(7);
  myservothree.attach(10);
  myservofour.attach(11);
  servomove();
  delay(1000);
  Serial.println("ready");
}

void loop() { 
  delay(x);
  setchangeangle();
  //Serial.println(xLchange);
  setservoangle();
  capservoangle();
  servomove();
  //print();
}


```
-


# First Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/aQ3g7442gqI?si=GySozU9xW-lcDUYO" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

My first milestone was contructing the frame of the arm. I installed the Arduino Nano board and the base of the arm to the base board. I attached all 4 servos to the chasis, the 2 joints, and the claw. The building process was rocky at first. I was missing a bag of screws that were vital for many of the joints, but luckily Bluestamp had the same size screw. I also accidentally broke a piece while trying to insert a bearing into one of the parts of the arm, but I was able to fix it with tape after a couple of tries. Despite all the inconveniences, this milestone went relatively smooth. 

# Schematics 
[schematic](wiringdiagram.pdf)

<!---

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


# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |

# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)
-

-->

# Starter Project

<iframe width="560" height="315" src="https://www.youtube.com/embed/9XJgiP5lbAM?si=RNG3RObgSUzBcW8B" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

My starter project was the calculator. This project both challenged me and made me learn a lot about enginnering. Even though I knew practically nothing about engineering, I learned skills such as soldering, desoldering, and using the multimeter to make the calculator. I had to solder on the LED display, all the button sensors, the battery slot, and the USB port. I struggled on what to do because there were no instructions. For example, the frame of the calculator could not fit the hardware, so I had to rearrange the frame to fit it. Overall, this project was an important step to a more complex project. Next, I will be starting my main project, the Phone-Controlled Robotic Arm.
