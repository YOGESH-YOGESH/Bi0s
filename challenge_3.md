# Challenge 2
 
## Circuit

![2ARDUINO](<Screenshot 2024-04-18 at 9.39.42 PM.png>)

## Code

### Transmitter Arduino

``` cpp
#include <SoftwareSerial.h>
String inputchar;
String sendMessage;


void setup()
{
 Serial.begin(9600);
 Serial1.begin(9600);
}

void loop()
{
 while(Serial.available()>0)
 {
   char inputChar = Serial.read();
 if (inputChar == '\n') 
 {
  Serial1.println(sendMessage);
  sendMessage = "";
 }
  else 
 {
  sendMessage += inputChar;
 }
}
}
```

---

### Receiver Arduino 

``` cpp
#include <SoftwareSerial.h>
#include <LiquidCrystal_I2C.h>
#define I2C_ADDRESS 0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

LiquidCrystal_I2C lcd(I2C_ADDRESS, LCD_COLUMNS, LCD_LINES);
String recivedchar;

void setup()
{
  Serial.begin(9600);
  Serial1.begin(9600);
  lcd.begin(16, 2);
}

void loop()
{
  	while (Serial1.available() > 0) 
  	{
   		char receivedChar = Serial1.read();
 	}
  	lcd.setCursor(0,1);
  	lcd.print(recivedchar);
  	delay(1000);
}
```


## Explanation 

### Transmitter code:

In the Transmitter Arduino input is taken from the user which is stored as a string and that is Transmitted via ***UART Communication*** <code> Serial1.begin</code> which connects to the another arduino.

### Receiver Arduino:

In the receiver arduino the lcd is connected which is a I2C communication and the received message is stored in another string which is displayed by the LCD.

## Challenges Faced

- connecting two Arduino in **Wokwi**.
- Getting input from the user and store it in an array.

## Resources 
