//# CRUISE_CONTROL-
//Speed control using an ultrasonic sensor
const int trigPin = 11;
const int echoPin = 10;
const int buzzPin = 6;
const int redPin = 8;
const int whitePin = 9;
const int yellowPin = 12;


long duration;
float distance;

void setup() 
{
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT); 
  pinMode(buzzPin, OUTPUT);
  pinMode(redPin, OUTPUT);
  pinMode(whitePin, OUTPUT);
  pinMode(yellowPin, OUTPUT);
  pinMode(5,OUTPUT);
  Serial.begin(9600);
}

void loop() 
{
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  duration = pulseIn(echoPin, HIGH);
  distance = 0.034*(duration/2);

  if (distance < 10)
  {
    digitalWrite(buzzPin,HIGH);
    
  }
  else 
  {
    digitalWrite(buzzPin,LOW);
  }
  if(distance<=90&&distance>=60)
  {
  digitalWrite(whitePin, HIGH);
   digitalWrite(yellowPin, LOW);
    digitalWrite(redPin, LOW);}
    else if(distance<=60&&distance>=30)
    {
      digitalWrite(whitePin, LOW);
   digitalWrite(yellowPin, HIGH);
    digitalWrite(redPin, LOW);
    }
    else if(distance<=30&&distance>10){
    digitalWrite(whitePin, LOW);
   digitalWrite(yellowPin, LOW);
    digitalWrite(redPin, HIGH);}
     else if(distance<10&&distance>0){
    digitalWrite(whitePin, LOW);
   digitalWrite(yellowPin, LOW);
    digitalWrite(redPin, HIGH);   // turn the LED on (HIGH is the voltage level)
  delay(100);                       // wait for a second
  digitalWrite(redPin, LOW);    // turn the LED off by making the voltage LOW
  delay(100);  }
    else{
    digitalWrite(whitePin, LOW);
   digitalWrite(yellowPin, LOW);
    digitalWrite(redPin, LOW);}
     distance = map( distance,  0 , 90, 0 , 255);
    analogWrite( 5, distance);
    Serial.println(distance);
  
  delay(300);
}
