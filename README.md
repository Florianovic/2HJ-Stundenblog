# 2HJ-Stundenblog

### 4.12.19
Das neue Halbjahr startet und wir müssen uns ein neues Projekt überlegen. Im letzten halbjahr haben wir mit einem "Arduino UNO" eine "Useless-Box" gabaut. Viele andere aus unserem Kurs haben Computerspiele entwickelt und auch wir haben uns nun überlegt, uns daran zu versuchen. Die Entwicklungsumgebung "Unity" war uns schon vom Namen her bekannt und wir haben uns gleich in der ersten Stunde ein Tutorial dazu angeschaut.
https://www.youtube.com/watch?v=DZbQRw-ftnU

### 10.12.19
Heute haben wir uns Unity heruntergeladen und einen Acount erstellt. Wir haben ein erstes Projekt erstellt und versucht, das Tutorial durchzugehen.
https://www.youtube.com/watch?v=H7d2WfQ95ws 

### 11.12.19
Heute war in der Schule leider das Internet ausgefallen, weswegen wir gezwungen waren uns ohne Recherche oder Informationen über das Programm mit der Entwicklungsumgebung vertraut zu machen. 

### 12.12.19
Für unser Spiel wollten wir, wie auch eine Gruppe im letzten Halbjahr, unsere eigene Musik einfügen. Dafür hat sich Florian das Programm Fl-Studio runtergeladen und auch hier eine Tutorialreihe angefangen.
LINK
Tobias hat sich weiter über Unity informiert und am Tutorial weitergearbeitet.

### 18.12.19
Heute war Tobi nicht da und Florian hat sich weiter das Tutorial zu Fl-Studio angeschaut.
Um nun aber mit dem Computerspiel voran zu kommen hat Florian sich in der zweiten Hälfte der Stunde daran gemacht, das Problem mit den zu kleinen Texturen zu lösen. Leider hat er dabei keine Lösung gefunden.

### 19.12.19
Auch heute war Tobi nicht da und Florian hat weiterhin versucht Unity zu vertshen. Er hat nach weiteren Tutorials gesucht doch keins gefunden was die Fragen beantwortet und uns wirklich weiter bringt.

### 15.01.2020
Spontan kamen wir auf die Idee ein Spiel im Syle von Flappy-Bird zu erstellen.Florian war heute nicht da und Tobi hat sich ein Tutorial angeguckt, mit welchem man dieses Projekt über Unity verwirklichen kann. Dieses war recht komplex und hat die gesamte Stunde in Anspruch genommen.

### 16.01.2020
Diese Stunde hat Tobi ein online Tutorial durchgearbeitet, ebenfalls zu Flappy-Bird, welches durch setzen von einfachen Blöcken ein wirklich einfaches Programmieren ermöglicht. Allerdings war dieses Programm zum Ende der Stunde durchgearbeitet und ein Fertiges Flappy-Bird Spiel war geschaffen, sodass wir uns dazu entschieden diesen Versuch wegen seiner geringen Komplexität wieder einzustampfen. 

### 21.01.2020
Da wir nun schon viel Zeit in Unity gesteckt haben aber noch ganz am Anfang stehen und auf der Stelle treten haben wir uns entschlossen nach alternativen Entwicklungsumgebungen zu suchen. Wir entdeckten "Snap" und schauten uns Videos dazu auf YouTube an.
https://www.youtube.com/watch?v=kSLnwUuE3Xg

### 22.01.2020
Heute haben wir uns eine weitere Entwicklungsumgebung namens "Scratch" angeschaut und ein YouTube-Tutorial dazu angefangen.

### 23.01.2020
Nachdem wir uns nun mit einigen Programmen beschäftigt haben aber es nicht geschafft haben uns mit ihnen vernünftig auseinanderzusetzten und bis jetzt absolut keine Ergebnisse hatten, haben wir uns nun dazu entschieden das Projekt "Spiel entwickeln" aufzugeben. Stattdessen wollten wir nun doch lieber wieder etwas mit dem, uns bereits bekannten Arduino machen

### 28.01.2020
Neuanfang:
Wir haben uns überlegt einige neue Komponenten mit dem Arduino auszuprobieren und einen Arduino-Safe zu bauen. Dafür wollen wir ein Keypad und ein LCD-Display einbauen. Das ganze soll so funktionieren, dass wir über das Key-Pad einen Code eingeben, welcher auf dem LCD angezeigt wird und bei richtiger Eingabe einen Servo betätigt, welcher als "Verschluss" des Safes fungiert.

### 04.02.2020
Heute haben wir dasKeypad getestet. Die Tasten werden Erkannt und benannt
<p align="center"><img width="400px" src="https://github.com/Florianovic/2HJ-Stundenblog/blob/master/TestKeypad.PNG"></p>

### 05.02.2020
Für die nächste Komponente, den LCD-Monitor, haben wir uns einen Bauplan aus dem Internet gesucht und uns alle Bestandteile zusammengesucht. Leider haben wir kein kleines Potentiometer an der Schule weswegen wir ein sehr altes und großes aus der Physik benutzen wollen. Der Test ist für nächste Stunde geplant

### 06.02.2020
Wir haben die Schalung aufgebaut und einen Sketch aus dem Internet kopiert. DerMonitor funktioniert, der Text wird jedoch nicht angezeigt. Auch nach mehreren Versuchen und dem Verstellen des Potentiometers hat das LCD nur blau geleuchtet aber keine Symbole gezeigt.

### 12.02.2020

Wir haben eine Aufgabenteilung vorgenommen um schneller voran zu kommen. Tobiversucht nun das LCD-Display zum Laufen zu bekommen und Florian erstellt den Sketch fü das Keypad.
Florian hat ein Sketch kopiert um dessen Aufbau zu verstehen.

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
Wir haben ein Problem:Wir haben zu wenig Pins am Arduino für LCD-Display, Keypad und Servo.
Um das zu lösen wollen wir von unserem ArduinoUNO auf ein Arduino Mega umsteigen, welcher deutlich mehr Pins hat.
Um es zu testen haben wir Keypad und Servo vom letzten Mal an den Arduino mega angeschlossen,den selben Code eingefügt und es hat funktioniert.

### 14.02.2020
Wir haben heute weiter probiert das LCD-Display zum laufen zu bringen, leider weiterhin erfolglos. Wir haben verschiedenste Verkabelungen und Codes ausprobiert, versucht eine Batterie als Spannungsquelle anzuschließen. Leider hat alles nicht zu einem Weiterführenden Ergebnis geführt. Des Weiteren versuchten wir über eine Umstellung des Kontrastes durch Variablen einen Schritt in die Richtige Richtung zu tun, leider ebenso ohne Erfolg

### 19.02.2020
Heute haben wir einen weiteren <a href="https://create.arduino.cc/projecthub/zurrealStudios/lcd-backlight-and-contrast-control-6d3452"> Bauplan</a> versucht nachzubauen. Leider blieb auch dieser Versuch ergebnislos, der Monitor zeigte erneut nur flackernd Felder an, wir vermuten, dass der Monitor defekt ist. Der Kontrast des Hintergrunds lässt sich hingegen durch das Potentiometer problemlos verstellen. Herr Buhl hat einen neuen LCD-Display bestellt, sowie kleinere, handliche Potentiometer. Diese sollten in den nächsten Stunden verfügbar sein.

### 20.02.2020
Da wir immer noch auf die neuen Teile warten haben wir uns dazu entschlossen unsere freie Zeit zu nutzen und den Stundenblog auszubessern.

### 06.03.2020
Heute war Tobi nicht da aber die Lieferung ist angekommen. Ein neues, kleineres LCD und ein kleines Potentiometer. Da das neue LCD weniger Pins hat, ist Florian wieder auf den ArduinoUNO umgestiegen und hat mit dem alten Bauplan versucht die Teile zu testen. Leider ohne Erfolg.

### 11.03.2020
Auch heute haben wir vergeblich versucht das neue LCD zum Laufen zu bringen. Wir haben viele verschiedene Codes aus dem Internet ausprobiert, auf mehreren Geräten die Library installiert und den Sketch geschrieben aber alles blieb erfolglos.

### 13.03.2020
Corona steht vor der Tür und die Chancen stehen sehr hoch, dass ab Montag kein Unterricht mehr ist. Wir haben uns also dazu entschlossen unsere Arbeit aufzuteilen und die Materialien mit nach Hause zu nehmen. Florian wird das Stundenprotokoll weiter ausarbeiten, Tobi nimmt die Hardware mit und wird versuchen den LCD zum laufen zu bringen.

### 19.03.2020
Dennis hat mich unerwartet angeschrieben mit der Nachricht, das er seinen LCD zum laufen gebracht habe und ob wir noch Hilfe benötigen. Ich habe dankend angenommen, worauf mich Dennis auf ihr Stundenprotokoll zu ihrem Teeautomat verwies.

### 20.03.2020
Heute habe ich versucht den LCD zum laufen zu bringen und habe exakt den Code, welchen Dennis mir geschickt hat abgetippt. Leider funktioniert der LCD immer noch nicht - vielleicht habe ich das Ganze falsch verkabelt? Ich habe Dennis erneut angeschrieben und nachgefragt. Die Antwort kam schnell, anscheinend habe ich alles richtig verkabelt. Ich habe sowohl den Arduino Uno als auch den Arduino Mega 2560 angeschlossen um auszuschließen, dass hier kein Fehler/Beschädigung vorliegt. Morgen werde ich weiter versuchen den LCD zum laufen zu bringen, allerdings fallen mir momentan keine weiteren möglichen Fehlerquelen ein.

### 22.03.2020
Ich habe weiter überlegt was der Fehler sein könnte. Die einzige Fehlerquelle, welche mir noch einfällt ist, dass ich falsche oder veraltete librarys habe und somit nicht alles Funktioniert. Allerings Zeigt die Konsole des Arduino an, dass der Code fehlerfrei abgelesen werden kann. Mir fällt keine andere Möglichkeit mehr ein, villeicht kommen mir in den nächsten Tagen noch ein paar Ideen.
