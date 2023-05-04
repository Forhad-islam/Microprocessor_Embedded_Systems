#include <Servo.h>   //servo library
Servo servo;
Servo servo2;   
int trigPin =8;    
int echoPin =9;   
int servoPin =7;
//int led=13;
long duration, dist, average;   
long aver[3];   //array for average

// 2nd servey 2 & supersonic sensor
int trigPin2 =10;    
int echoPin2 =11;   
int servoPin2 =6;
//int led2=4 ;
long duration2, dist2, average2;   
long aver2[3];   //array for average 

// for flame sensor
const int ledpin=13;  
const int flamepin=A2;
const int buzpin=12;
const int threshold=200;// sets threshold value for flame sensor
int flamesensvalue=0; // initialize flamesensor reading 


void setup() {       
    Serial.begin(9600);
    servo.attach(servoPin);  
   // pinMode(led, OUTPUT);
    pinMode(trigPin, OUTPUT);  
    pinMode(echoPin, INPUT);  
    servo.write(0);         //close cap on power on
    delay(100);
    servo.detach(); 

    //for flame sensor
    pinMode(ledpin,OUTPUT);
    pinMode(flamepin,INPUT);
    pinMode(buzpin,OUTPUT); 

    //2nd servey $ sensor
    Serial.begin(4800);
    servo2.attach(servoPin2);  
    //pinMode(led2, OUTPUT);
    pinMode(trigPin2, OUTPUT);  
    pinMode(echoPin2, INPUT);  
    servo2.write(0);         //close cap on power on
    delay(100);
    servo2.detach();  
} 

void measure() {  

digitalWrite(trigPin, LOW);
delayMicroseconds(5);
digitalWrite(trigPin, HIGH);
delayMicroseconds(15);
digitalWrite(trigPin, LOW);
pinMode(echoPin, INPUT);
duration = pulseIn(echoPin, HIGH);
dist = (duration/2) / 29.1;    //obtain distance

}

void measure2()
{
  // for 2nd servey motor and sensor, led

digitalWrite(trigPin2, LOW);
delayMicroseconds(5);
digitalWrite(trigPin2, HIGH);
delayMicroseconds(15);
digitalWrite(trigPin2, LOW);
pinMode(echoPin2, INPUT);
duration2 = pulseIn(echoPin2, HIGH);
dist2 = (duration2/2) / 29.1;    //obtain distance
}


void loop() { 
  for (int i=0;i<=2;i++) {   //average distance
    measure();               
   aver[i]=dist;            
    delay(10);              //delay between measurements
  }

    // for loop for 2nd sensor and others 
     for (int i=0;i<=2;i++) {   //average2 distance
    measure2();               
   aver2[i]=dist2;            
    delay(10);              //delay between measurements
     }

  //use for flame sensor loop 
  flamesensvalue=analogRead(flamepin); // reads analog data from flame sensor
if (flamesensvalue<=threshold) { // compares reading from flame sensor with the threshold value
digitalWrite(ledpin,HIGH); //turns on led and buzzer
tone(buzpin,100);
delay(1000); //stops program for 1 second
}
else{
digitalWrite(ledpin,LOW); //turns led off led and buzzer
noTone(buzpin);
} 

  
 dist=(aver[0]+aver[1]+aver[2])/3;     // ok for 1 motor 
 dist2=(aver2[0]+aver2[1]+aver2[2])/3;   // ok for 2nd motor 

if ( dist<20 ) {
//Change distance as per your need
 servo.attach(servoPin);
  delay(1);
 servo.write(0);  
 delay(2000);       
 servo.write(90);
 //digitalWrite (led , HIGH );   
 delay(1000);
 servo.detach();    
   
}
else
{
 // digitalWrite (led, LOW );
}

// for 2nd motor and sensor 
if ( dist2<5) {
//Change distance as per your need
 servo2.attach(servoPin2);
  delay(1);
 servo2.write(0);  
 delay(2000);       
 servo2.write(90);
 //digitalWrite (led2 , HIGH );   
 delay(1000);
 servo2.detach();    
   
}
else
{
  //digitalWrite (led2, LOW );
}
Serial.println(dist2);
}
