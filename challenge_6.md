# Challenge 2

## Circuit

![16x2 LCD](<Screenshot 2024-04-14 at 1.16.37 AM.png>)

## Explanation

```
1000 0000 (clear display)
0100 0000 (return home)
(111)1 0000 (display,cursor,cursor blink)(on/off)
(001)1 0000 (8/4 bit,line,size)(on/off)
RS - 1
xxxx xxxx (data)
b -0100 0110
i -1001 0110
0 -0000 1100
s -1100 1110
H -0001 0010
a -1000 0110
r -0100 1110
d -0010 0110
w -1110 1110
a -0001 0110
r -0100 1110
e -1010 0110
```

- **<span style="color: red;">VSS</span>** and **<span style="color: grey;">VDD</span>** are connected to ground and vcc accordingly
- **<span style="color: green;">RS</span>** is set to 0 initially to setup the LCD and turned to 1 while sending Data.
- **<span style="color: fuchsia;">RW</span>** is set to 0 since we are only writing Data to LCD.
- **<span style="color: aquamarine;">E</span>** is used to control the LCD.
- **<span style="color: pink;">D0-D7</span>** are used to send data.

## Resources