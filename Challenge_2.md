# Challenge 2

## Circuit

![Bare metal](<Screenshot 2024-04-18 at 7.30.29 PM.png>)

## Given code

```c
#define DDRB *((volatile byte*) 0x24)//DDRB Address
#define PORTB *((volatile byte*) 0x25)//PORTB Address
#define PINB *((volatile byte*) 0x23)//PINB Address
#define mc "atmega328p"

void setup()
{
  DDRB = (1<<5);    //00100000
  DDRB &= ~(1<<4);  //00010000
  PORTB |= (1<<4);  //00010000
}

void loop()
{
  if(!(PINB & (1<<4)))  //00010000
  {
    PORTB |= (1<<5);    //00100000
  }
  else
  {
    PORTB &= ~(1<<5);   //11011111
  }
  delay(10);
}
``` 

## Reduced Code

```cpp
int a;
void setup()
{
  pinMode(13, OUTPUT);
  pinMode(12, INPUT);
}

void loop()
{
  a=digitalRead(12);
  if(!(a))
  {
    digitalWrite(13, HIGH);
  }
  else
  {
    digitalWrite(13, LOW);
  }
  delay(10);
}
```

## Explanation

- **<span style="color: red;">DDRB</span>** refers to **<span style="color: red;">pinMode</span>** 
- **<span style="color: cyan;">PORTB</span>** refers to **<span style="color: cyan;">digitalWrite</span>**

- **<span style="color:fuchsia ;">PINB</span>** refers to **<span style="color:fuchsia ;">Input Pin Address</span>**

---

- ```DDRB = (1<<5);``` == ```pinMode(13, OUTPUT);```

- ```DDRB &= ~(1<<4);``` == ```pinMode(12, INPUT);```

- ```PORTB |= (1<<4);``` == ```digitalRead(12);```

## Resources


