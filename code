#include <DHT.h>
#include <LiquidCrystal_I2C.h>


#define DHTPIN 8
#define DHTTYPE DHT22


DHT dht(DHTPIN, DHTTYPE);
LiquidCrystal_I2C lcd(0x27, 16, 2);


const int pirPin = A1;
const int redPin = 4;
const int greenPin = 3;
const int bluePin = 5;
const int buzzerPin = 2;


void setup() {
 lcd.init();
 lcd.backlight();
 pinMode(pirPin, INPUT);
 pinMode(redPin, OUTPUT);
 pinMode(greenPin, OUTPUT);
 pinMode(bluePin, OUTPUT);
 digitalWrite(bluePin,LOW);
 pinMode(buzzerPin, OUTPUT);
 Serial.begin(9600);
 dht.begin();


 // the LCD calibrates and delays the start of the rest of
 // the code for 12 seconds meanwhile.
 lcd.clear();
 lcd.setCursor(0, 0);
 lcd.print("Calibrating...");
 lcd.setCursor(0, 1);
 lcd.print("Please wait...");


 delay(12000); // Delay for 12 seconds before starting the code


 lcd.clear();
 lcd.setCursor(0, 0);
 lcd.print("Temperature:");
}


void loop() {
//DHT Code
 float temperature = dht.readTemperature();


 lcd.clear();             // Clear the LCD display
 lcd.setCursor(0, 0);     // Set the cursor to the first column, first row
 lcd.print("Temperature:"); // Print the label "Temperature:"
 lcd.setCursor(0, 1);     // Set the cursor to the first column, second row
 lcd.print(temperature);   // Print the temperature value


 if (!isnan(temperature)) {
   Serial.print("Temperature: ");
   Serial.print(temperature);
   Serial.println(" degrees Celsius");


   if (temperature > 20) {
     // Adjust RGB colors here
     int redValue = 0;    // No red
     int greenValue = 255;  // Maximum green value
     int blueValue = 0;     // No blue
    
     analogWrite(redPin, redValue);
     analogWrite(greenPin, greenValue);
     analogWrite(bluePin, blueValue);
    
     tone(buzzerPin, 1000);
     delay(1000);
     digitalWrite(redPin, LOW);
     digitalWrite(greenPin, LOW);
     digitalWrite(bluePin, LOW);
     noTone(buzzerPin);
     delay(1000);
   } else {
     digitalWrite(redPin, LOW);
     digitalWrite(greenPin, LOW);
     digitalWrite(bluePin, LOW);
   }
     if (digitalRead(pirPin) == HIGH) {
     digitalWrite(redPin, LOW);
     digitalWrite(greenPin, LOW);
     digitalWrite(bluePin, HIGH);
     delay(2000);
     digitalWrite(bluePin, LOW);
   } else {
   if (digitalRead(pirPin)== LOW) {
       digitalWrite(bluePin, LOW);
     }
   }
 }


 delay(3500);
}
