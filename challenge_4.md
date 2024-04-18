# Challenge 4

## Circuit
![KEYPAD](<Screenshot 2024-04-18 at 9.38.00 PM.png>)
## Code

``` cpp
#include <Keypad.h>
#include <Servo.h>
#include <SPI.h>
#include <Wire.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>

#define SCREEN_WIDTH 128 
#define SCREEN_HEIGHT 64 
#define SERVO_PIN  A1

#define OLED_RESET  -1 
#define SCREEN_ADDRESS 0x3C
Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, OLED_RESET);

Servo servo;
char keys[4][4] = {
  {'1', '2', '3', 'A'},
  {'4', '5', '6', 'B'},
  {'7', '8', '9', 'C'},
  {'*', '0', '#', 'D'}
};
byte pin_rows[4] = {9, 8, 7, 6};
byte pin_column[4] = {5, 4, 3, 2};
Keypad keypad = Keypad( makeKeymap(keys), pin_rows, pin_column, 4, 4 );
const String password = "12345678";
String input_password;
int angle = 0;

unsigned long lastTime;
void setup() {
  Serial.begin(9600);
  input_password.reserve(32);
  servo.attach(SERVO_PIN);
  servo.write(0);

  if(!display.begin(SSD1306_SWITCHCAPVCC, SCREEN_ADDRESS)) 
  {
    Serial.println(("Display ready"));
    for(;;);
  }
}
void loop() 
{
  char key = keypad.getKey();
  if (key) 
  {
    Serial.println(key);
    if (key == '*') 
    {
      input_password = "";
    } 
    else if (key == '#') 
    {
      if (input_password == password) 
      {
        Serial.println("The password is correct");
        display.setTextSize(1);
        display.setTextColor(WHITE);
        display.setCursor(0,28);
        display.println("OPEN");
        display.display();
        delay(1000);
        display.clearDisplay();
        servo.write(90);
        delay(5000);
        servo.write(0);
      } 
      else 
      {
        Serial.println("The password is incorrect, try again");
        display.setTextSize(1);
        display.setTextColor(WHITE);
        display.setCursor(0,28);
        display.println("close");
        display.display();
        delay(2000);
        display.clearDisplay();
      }
      input_password = ""; 
    } 
    else 
    {
      input_password += key;
    }
  }
}
```
## Explanation

### Keypad:

- Keypad library is included.
- A 2D array is used to assign the keypad structure.
- Pin_rows and Pin_column arrays are used for arduino connection.
- makekeymap initialize the keypad keymap to user define keymap.
- getkey is used to get key whenever the key is pressed.

### Servo:

- Servo library is included.
- Servo pin is connected to A0.

### Oled Display:

- SCL (Serial Clock Pin) and SDA (Serial Analog Pin) is connected to A4 and A5.
- <code> #include <Wire.h></code> is used for I2c communication.
- <code> #include <spi.h></code> is used for faster communication within the devices.
- <code> #include <Adafruit_SSD1306.h></code> and <code> #include <Adafruit_GFX.h> </code> Oled led library are used.

- Dimentions of the Oled display is defined and since it doesn't have a reset pin, -1 is used to reset the oled display and address of the oled is also defined.

---

- The password is set in the code and when the code runs using getkey, whenever the user presses the key it is stored in a string and when **#** is pressed means the user typed the password and it's tells to check with the password given.  when **\*** is pressed the stored input password resets and starts from the first.
- If the password is correct then the servo is turned to 90 degree and the oled displays OPEN and this lasts upto 5 seconds.
- if the password is wrong then the servo stays in 0 degree and the led displays CLOSE. 

## Challenges Faced

- Setting the Oled display.
- While merging all the codes (since I coded them in order of Keypad, Servo, Oled Display).

## Resources