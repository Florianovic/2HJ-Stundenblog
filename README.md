# 2HJ-Stundenblog

### 4.12.19
Wir haben uns überlegt ein Spiel zu machen
um das zu verwirklichen wollen wir Unity als Etwicklungsumgeung nutzen

### 10.12.19
Unity Acount erstellt, erstes Pfrojekt erstellt
https://www.youtube.com/watch?v=H7d2WfQ95ws angeschaut

### 11.12.19
ohne Internet bissn unity probiert

### 12.12.19
Flo: Fl-Studio ausprobiert
Tobi: Unity Tutorial

### 18.12.19
ohne Tobi Unity tutorial reingezogen
### 19.12.19
ohne Tobi Unity Tutorial und ausprobiert

### Woche wo Flo nicht da war
### 15.01.2020
Tutorial zu Flappy bird geguckt
### 16.01.2020
Flappy bird online tutorial durchgearbeitet, zu einfach
### 21.01.2020
Tutorial zu Flappy bird und Snap angeguckt
### 22.01.2020
Tutorial zu scratch und snap angeguckt
### 23.01.2020
tutorial zu scratch, realisierbarkeit des Projektes geprüft

### 28.01.2020
Neuanfang:Arduino Safe bauen mit Keypad und LCD-Display  

### 04.02.2020
Test des Keypads, Tasten werden Erkannt und benannt
<p align="center"><img width="400px" src="https://github.com/Florianovic/2HJ-Stundenblog/blob/master/TestKeypad.PNG"></p>

### 05.02.2020
LCD-Monitor Bauplan erstellt, Test für nächste Stune geplant

### 06.02.2020
Monitor funktioniert, Text wird aber nicht angezeigt

### 12.02.2020
>Aufgabenteilung, Tobi:LCD-Display, Flo: Keypad
Flo:
Code kopiert:
#include <Keypad.h>
#include <Servo.h> 

// Pinlänge und Pincode festlegen
const byte PINLENGTH = 4;
char pinCode[PINLENGTH+1] = {'0','8','1','5'};

// Zwischenspeicher für Eingaben
char keyBuffer[PINLENGTH+1] = {'-','-','-','-'};

// Kompakter kann man das auch so schreiben:
// char pin[] = "0815";
// char keyBuffer[] = "----";

// Definition für das Keypad von Elegoo
const byte ROWS = 4; // vier Zeilen
const byte COLS = 4; // vier Spalten
// Symbole auf den Tasten
char hexaKeys[ROWS][COLS] = {
  {'1','2','3','A'},
  {'4','5','6','B'},
  {'7','8','9','C'},
  {'*','0','#','D'}
};
byte rowPins[ROWS] = {9, 8, 7, 6}; //connect to the row pinouts of the keypad
byte colPins[COLS] = {5, 4, 3, 2}; //connect to the column pinouts of the keypad

// Einstellung für Servo und LEDs
const int greenPin = 12;
const int redPin = 13;
const int servoPin = 11;
const int angleClosed = 30;
const int angleOpen = 120;
const int openDelay = 3000;

// Servo-Objekt erzeugen
Servo myservo;

// Instanz von Keypad erzeugen, Keymap und Pins übergeben
Keypad customKeypad = Keypad( makeKeymap(hexaKeys), rowPins, colPins, ROWS, COLS); 

void setup(){
  Serial.begin(9600);
  // LED Pins setzen
  pinMode(greenPin, OUTPUT);
  pinMode(redPin, OUTPUT);
  digitalWrite(greenPin, LOW);
  digitalWrite(redPin, LOW);
  // Servo auf Ausgangsposition
  myservo.attach(servoPin);
  myservo.write(angleClosed);
}
  
void loop(){
  // Gedrückte Taste abfragen
  char customKey = customKeypad.getKey();

  if (customKey) {
    // Check, ob ASCII Wert des Char einer Ziffer zwischen 0 und 9 entspricht
    if ((int(customKey) >= 48) && (int(customKey) <= 57)){ 
      addToKeyBuffer(customKey); 
    }
  // oder Code überprüfen, falls Raute gedrückt wurde 
    else if (customKey == '#') { 
      checkKey(); 
    } 
  } 
} 

void addToKeyBuffer(char inkey) { 
  Serial.print(inkey); 
  Serial.print(" > ");
  // Von links nach rechts Zeichen um eins weiterkopieren = ältestes Zeichen vergessen
  for (int i=1; i<PINLENGTH; i++) {
    keyBuffer[i-1] = keyBuffer[i];
  }
  // in ganz rechter Stelle die letzte Ziffer speichern
  keyBuffer[PINLENGTH-1] = inkey;
  Serial.println(keyBuffer);
}

void checkKey() {
  // Eingabe mit festgelegtem Pincode vergleichen
  if (strcmp(keyBuffer, pinCode) == 0) {
    Serial.println("CORRECT");
    // Aktion für richtigen Pin ausführen
    pinCorrect();
  }
  else {
    Serial.println("WRONG!");
    // Aktion für falschen Pin ausführen
    pinWrong();
  }

  // Nach Überprüfung Eingabe leeren
  for (int i=0; i < PINLENGTH; i++) {
    keyBuffer[i] = '-'; 
  }
}

// Aktion für korrekten Pincode
void pinCorrect() {
  myservo.write(angleOpen);
  digitalWrite(greenPin, HIGH);
  delay(openDelay);
  myservo.write(angleClosed);
  digitalWrite(greenPin, LOW);
}

// Aktion für falschen Pincode
void pinWrong() {
  for (int i=0; i<3; i++) {
    digitalWrite(redPin, HIGH);
    delay(50);
    digitalWrite(redPin, LOW);  
    delay(20);
  }
}

### 13.02.2020
Problem: zu wenig Pins am Arduino für LCD-Display, Keypad und Servo
Lösung: Arduino Mega
Mehr Pins
Ausprobiert, Keypad und Servo vom letzten Mal an Arduino mega angeschlossen, selber Code, FUNZT
