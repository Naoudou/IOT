# IOT

RGB

// C++ code
const int redPin = 9;
const int greenPin = 10;
const int bluePin = 11;

void setup() {
  pinMode(redPin, OUTPUT);
  pinMode(greenPin, OUTPUT);
  pinMode(bluePin, OUTPUT);
}

void loop() {
  // Red light on
  setColor(255, 0, 0); // Red
  delay(1000); 

  // Green light on
  setColor(0, 255,0 ); // Green
  delay(1000); 

  // Yellow light on
  setColor(0, 0, 255); // Yellow
  delay(1000); 
  
  
   
}

void setColor(int red, int green, int blue) {
  analogWrite(redPin, red);
  analogWrite(greenPin, green);
  analogWrite(bluePin, blue);
}





TRAFIC LIGHT

// C++ code
//
const int redLED = 10;
const int yellowLED = 9;
const int greenLED = 8;

void setup() {
  pinMode(redLED, OUTPUT);
  pinMode(yellowLED, OUTPUT);
  pinMode(greenLED, OUTPUT);
}

void loop() {
  // Red light on
  digitalWrite(redLED, HIGH);
  delay(5000); 

  // Green light on
  digitalWrite(redLED, LOW);
  digitalWrite(greenLED, HIGH);
  delay(5000); 

  // Yellow light on
  digitalWrite(greenLED, LOW);
  digitalWrite(yellowLED, HIGH);
  delay(2000);
  digitalWrite(yellowLED, LOW); 
}



MULTIPLE LED BLICK

// C++ code
//
// Define the pins for the LEDs
const int ledPins[] = {2, 3, 4, 5, 6, 7, 8, 9, 10, 11};
const int numLeds = 10;
const int delayTime = 100; // Delay time in milliseconds

void setup() {
  // Initialize all pins as outputs
  for (int i = 0; i < numLeds; i++) {
    pinMode(ledPins[i], OUTPUT);
  }
}

void loop() {
  // Turn on the LEDs one by one
  for (int i = 0; i < numLeds; i++) {
    digitalWrite(ledPins[i], HIGH);
    delay(delayTime);
  }

  // Turn off the LEDs one by one
  for (int i = 0; i < numLeds; i++) {
    digitalWrite(ledPins[i], LOW);
    delay(delayTime);
  }
}






DETECTION OBJECT USING ULTRA SONIC


// C++ code
const int trigPin = 9;
const int echoPin = 10;
const int relayPin = 8;

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(relayPin, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  long duration, distance;
  
  // Clear the trigPin by setting it LOW
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);

  // Trigger the sensor by setting trigPin HIGH for 10 microseconds
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  // Read the echoPin, and calculate the distance
  duration = pulseIn(echoPin, HIGH);
  distance = (duration / 2) / 29.1;

  // Print the distance to the Serial Monitor
  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");

  // If the distance is less than 30 cm, turn on the light bulb
  if (distance < 50) {
    digitalWrite(relayPin, HIGH);
  } else {
    digitalWrite(relayPin, LOW);
  }

  delay(100); // Delay before the next reading
}


FIRE ALARM GAZ DETECTION

float temp;
float vout;
float vout1;
int LED =13;
int gasSensor;
int piezo=7;
void setup()
{
  pinMode(A0,INPUT);
  pinMode(A1,INPUT);
  pinMode(A1,OUTPUT);
  pinMode(piezo,OUTPUT);
  Serial.begin(9600);
}
void loop()
{
  vout=analogRead(A1);
  vout1=(vout/1023)*5000;
  temp=(vout1-500)/10;
  gasSensor=analogRead(A0);
  if(temp>=80)
  {
    digitalWrite(LED,HIGH);
  }
  else
  {
    digitalWrite(LED,LOW);
  }
  if(gasSensor>=100)
  {
    digitalWrite(piezo,HIGH);
  }
  else
  {
    digitalWrite(piezo,LOW);
  }
  Serial.print("in Degree C= ");
  Serial.print(" ");
  Serial.print(temp);
  Serial.print("\t");
  Serial.print("GasSensor =");
  Serial.print(" ");
  Serial.print(gasSensor);
  Serial.println();
  delay(1000);
}



AUTOMATIC STREET LIGHT

// C++ code
//
int led=8;
int ldr=A0;
void setup()
{
  Serial.begin(9600);
  pinMode(ldr,INPUT);
  pinMode(led,OUTPUT);
}

void loop()
{
  int ldrval=analogRead(ldr);
  Serial.println(ldrval);
  if(ldrval>500)
  {
    digitalWrite(led,HIGH);
  }
  else
  {
    digitalWrite(led,LOW);
  }
}


MOTION DETECTION

const int pirPin = 2;      // Broche numérique où le capteur PIR est connecté
const int ledPin = 7;      // Broche où la LED est connectée
const int buzzerPin = 8;   // Broche où le buzzer est connecté

int pirState = LOW;        // État actuel du capteur PIR
int val = 0;               // Variable pour stocker la valeur lue du capteur PIR

void setup() {
  pinMode(pirPin, INPUT);    // Capteur PIR configuré comme entrée
  pinMode(ledPin, OUTPUT);   // LED configurée comme sortie
  pinMode(buzzerPin, OUTPUT);// Buzzer configuré comme sortie
  Serial.begin(9600);        // Initialisation de la communication série
}

void loop() {
  val = digitalRead(pirPin);  // Lecture de la valeur du capteur PIR

  if (val == HIGH) {
    if (pirState == LOW) {
      Serial.println("Mouvement détecté!");  // Affiche un message sur le moniteur série
      digitalWrite(ledPin, HIGH);  // Allumer la LED
      digitalWrite(buzzerPin, HIGH);  // Activer le buzzer
      pirState = HIGH;  // Met à jour l'état du capteur PIR
    }
  } else {
    if (pirState == HIGH) {
      Serial.println("Pas de mouvement");
      digitalWrite(ledPin, LOW);  // Éteindre la LED
      digitalWrite(buzzerPin, LOW);  // Désactiver le buzzer
      pirState = LOW;  // Met à jour l'état du capteur PIR
    }
  }

  delay(1000);  // Délai d'une seconde entre chaque lecture pour éviter les fausses détections
}









// C++ code
//
int moisture = 0;

void setup()
{
  pinMode(A0, OUTPUT);
  pinMode(A1, INPUT);
  Serial.begin(9600);
  pinMode(8, OUTPUT);
  pinMode(9, OUTPUT);
  pinMode(10, OUTPUT);
  pinMode(11, OUTPUT);
  pinMode(12, OUTPUT);
}

void loop()
{
  // Apply power to the soil moisture sensor
  digitalWrite(A0, HIGH);
  delay(10); // Wait for 10 millisecond(s)
  moisture = analogRead(A1);
  // Turn off the sensor to reduce metal corrosion
  // over time
  digitalWrite(A0, LOW);
  Serial.println(moisture);
  digitalWrite(8, LOW);
  digitalWrite(9, LOW);
  digitalWrite(10, LOW);
  digitalWrite(11, LOW);
  digitalWrite(12, LOW);
  if (moisture < 200) {
    digitalWrite(12, HIGH);
  } else {
    if (moisture < 400) {
      digitalWrite(11, HIGH);
    } else {
      if (moisture < 600) {
        digitalWrite(10, HIGH);
      } else {
        if (moisture < 800) {
          digitalWrite(9, HIGH);
        } else {
          digitalWrite(8, HIGH);
        }
      }
    }
  }
  delay(100); // Wait for 100 millisecond(s)
}








// C++ code
//
#include<IRremote.hpp>
const int rcvPin=8;
IRrecv irrecv(rcvPin);


int irr=7;
void setup()
{
  Serial.begin(9600);
  pinMode(irr, INPUT);
}

void loop()
{
  
   if(IrReceiver.decode()){
    auto value=IrReceiver.decodedIRData.decodedRawData;
   	Serial.println("le code du bouton est:");
  	Serial.println(value);
     IrReceiver.resume();
   }
  
  delay(100); // Wait for 1000 millisecond(s)
}










float temp;
float vout;
float vout1;
int LED =13;
int gasSensor;
int piezo=7;
void setup()
{
  pinMode(A0,INPUT);
  pinMode(A1,INPUT);
  pinMode(A1,OUTPUT);
  pinMode(piezo,OUTPUT);
  Serial.begin(9600);
}
void loop()
{
  vout=analogRead(A1);
  vout1=(vout/1023)*5000;
  temp=(vout1-500)/10;
  gasSensor=analogRead(A0);
  if(temp>=80)
  {
    digitalWrite(LED,HIGH);
  }
  else
  {
    digitalWrite(LED,LOW);
  }
  if(gasSensor>=100)
  {
    digitalWrite(piezo,HIGH);
  }
  else
  {
    digitalWrite(piezo,LOW);
  }
  Serial.print("in Degree C= ");
  Serial.print(" ");
  Serial.print(temp);
  Serial.print("\t");
  Serial.print("GasSensor =");
  Serial.print(" ");
  Serial.print(gasSensor);
  Serial.println();
  delay(1000);
}










// C++ code
//

const int tempPin = A0;  // Pin du capteur LM35
const int fanPin = 9;    

void setup() {
  Serial.begin(9600);  
  pinMode(fanPin, OUTPUT);  
}

void loop() {
  int tempValue = analogRead(tempPin);  // Lire la valeur analogique du LM35
  float temperature = (tempValue * 5.0 * 100.0) / 1024.0;  // Convertir en degrés Celsius
  
  
  Serial.print("Temperature: ");
  Serial.print(temperature);
  Serial.println(" *C");
  
  // Régulation de la vitesse du ventilateur
  int fanSpeed = map(temperature, 20, 40, 0, 255);  // Ajuster les valeurs pour tes besoins
  fanSpeed = constrain(fanSpeed, 0, 255);  // Limiter la vitesse entre 0 et 255
  analogWrite(fanPin, fanSpeed);  // Appliquer la vitesse au ventilateur

  delay(1000);  // Pause avant la prochaine lecture
}













const int pirPin = 2;      
const int ledPin = 7;      
const int buzzerPin = 8;  

int pirState = LOW;        
int val = 0;               
void setup() {
  pinMode(pirPin, INPUT);    
  pinMode(ledPin, OUTPUT);   
  pinMode(buzzerPin, OUTPUT);
  Serial.begin(9600);        
}

void loop() {
  val = digitalRead(pirPin);  

  if (val == HIGH) {
    if (pirState == LOW) {
      Serial.println("Mouvement détecté!");  
      digitalWrite(ledPin, HIGH);  
      digitalWrite(buzzerPin, HIGH);  
      pirState = HIGH;  
    }
  } else {
    if (pirState == HIGH) {
      Serial.println("Pas de mouvement");
      digitalWrite(ledPin, LOW);  
      digitalWrite(buzzerPin, LOW);  
      pirState = LOW;  
    }
  }

  delay(1000);  
}


















// C++ code
const int trigPin = 9;
const int echoPin = 10;
const int relayPin = 8;

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(relayPin, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  long duration, distance;
  
  // Clear the trigPin by setting it LOW
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);

  // Trigger the sensor by setting trigPin HIGH for 10 microseconds
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  // Read the echoPin, and calculate the distance
  duration = pulseIn(echoPin, HIGH);
  distance = (duration / 2) / 29.1;

  // Print the distance to the Serial Monitor
  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");

  // If the distance is less than 30 cm, turn on the light bulb
  if (distance < 50) {
    digitalWrite(relayPin, HIGH);
  } else {
    digitalWrite(relayPin, LOW);
  }

  delay(100); // Delay before the next reading
}














#include<Adafruit_LiquidCrystal.h>
#include<Servo.h>
int pir_sensor=0;
Adafruit_LiquidCrystal lcd_1(0);
Servo servo_6;
void setup()
{
  pinMode(3,INPUT);
  Serial.begin(9600);
  lcd_1.begin(16,2);
  servo_6.attach(6,500,2500);
  
  
}
void loop()
{
  pir_sensor=digitalRead(3);
  lcd_1.setCursor(0,0);
  Serial.println(pir_sensor);
  if(pir_sensor == 1){
    lcd_1.setCursor(0,1);
    servo_6.write(90);
    lcd_1.print("Door open   ");
  }else{
    lcd_1.setCursor(0,1);
    servo_6.write(0);
    lcd_1.print("Door close  ");
  }
  delay(100);
}










