# Robo-Maze-Solver
Robo Maze Solver

#define trigPin1 A0
#define echoPin1 A1
#define trigPin2 A2
#define echoPin2 A3
#define trigPin3 A4
#define echoPin3 A5


 //adjust this value to change the speed of the robot

void setup() {
  pinMode(trigPin1, OUTPUT);
  pinMode(echoPin1, INPUT);
  pinMode(trigPin2, OUTPUT);
  pinMode(echoPin2, INPUT);
  pinMode(trigPin3, OUTPUT);
  pinMode(echoPin3, INPUT);

  
  Serial.begin(9600); //initialize serial communication
}

void loop() {
  long duration1, duration2, duration3, distance1, distance2, distance3;

  digitalWrite(trigPin1, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin1, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin1, LOW);
  duration1 = pulseIn(echoPin1, HIGH);
  distance1 = duration1 * 0.034 / 2;

  digitalWrite(trigPin2, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin2, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin2, LOW);
  duration2 = pulseIn(echoPin2, HIGH);
  distance2 = duration2 * 0.034 / 2;

  digitalWrite(trigPin3, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin3, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin3, LOW);
  duration3 = pulseIn(echoPin3, HIGH);
  distance3 = duration3 * 0.034 / 2;

  Serial.print(distance1);
  Serial.print(" ");
  Serial.print(distance2);
  Serial.print(" ");
  Serial.println(distance3);

  if(distance1 > 15 && distance2 > 10 && distance3 > 10){ //if no obstacle in front of the robot
    moveForward();
  }
  else if(distance1 > 15 && distance2 <= 10 && distance3 <= 10){ //if obstacles on the left and in front of the robot
   moveForward();
  }
  else if(distance1 > 15 && distance2 > 10 && distance3 <= 10){ //if obstacle in front of the robot
    turnLeft();
  }
  else if(distance1 > 15 && distance2 <= 10 && distance3 > 10){ //if obstacle on the right of the robot
    turnRight();
  }
  else if(distance1 <= 15 && distance2 > 10 && distance3 > 10){ //if obstacle on the left of the robot
    turnLeft();
  }
  else if(distance1 > 15 && distance2 <= 10 && distance3 <= 10){ //if obstacles on the right and in front of the robot
    turnLeft(); 
  }
  else if(distance1 <= 15 && distance2 > 10 && distance3 <= 10){ //if obstacles on the left and in front of the robot
    turnRight();
  }
 else if(distance1 < 15 && distance2 > 10 && distance3 > 10){ //if obstacle in front of the robot
  moveBackward();
 }
 else if(distance1 > 15 && distance2 <= 10 && distance3 > 10){ //if obstacle on the right of the robot
  pivotRight();
 }
 else if(distance1 <= 15 && distance2 > 10 && distance3 > 10){ //if obstacle on the left of the robot
  pivotLeft();
 }

  else{ //if obstacles on both sides of the robot
    stopRobot();
  }
 }

 void moveForward(){
  digitalWrite(8, LOW);
  digitalWrite(9, HIGH);
  digitalWrite(10, LOW);
  digitalWrite(11, HIGH);
  analogWrite(5, 250);
  analogWrite(6, 250);
}
void moveBackward(){
  digitalWrite(8, HIGH);
  digitalWrite(9, LOW);
  digitalWrite(10, HIGH);
  digitalWrite(11, LOW);
  analogWrite(5, 250);
  analogWrite(6, 250);
   delay(1500); //adjust this value to change the duration of the turn
  stopRobot();
}

void turnLeft(){
  digitalWrite(8, HIGH);
  digitalWrite(9, LOW);
  digitalWrite(10, LOW);
  digitalWrite(11, HIGH);
  analogWrite(5, 250);
  analogWrite(6, 250);
  delay(800); //adjust this value to change the duration of the turn
  stopRobot();
}

void turnRight(){
digitalWrite(8, LOW);
digitalWrite(9, HIGH);
digitalWrite(10, HIGH);
digitalWrite(11, LOW);
analogWrite(5, 250);
analogWrite(6, 250);
delay(800); //adjust this value to change the duration of the turn
stopRobot();
}
void pivotLeft(){
  digitalWrite(8, HIGH);
  digitalWrite(9, LOW);
  digitalWrite(10, LOW);
  digitalWrite(11, LOW);
  analogWrite(5, 200);
  analogWrite(6, 200);
  delay(800); //adjust this value to change the duration of the turn
  stopRobot();
}

void pivotRight(){
  digitalWrite(8, LOW);
  digitalWrite(9, LOW);
  digitalWrite(10, HIGH);
  digitalWrite(11, LOW);
  analogWrite(5, 200);
  analogWrite(6, 200);
  delay(800); //adjust this value to change the duration of the turn
  stopRobot();
}


void stopRobot(){
digitalWrite(8, LOW);
digitalWrite(9, LOW);
digitalWrite(10, LOW);
digitalWrite(11, LOW);
}
