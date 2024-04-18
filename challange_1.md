# CHALLENGE 1

## Circuit
![image](https://github.com/weanysel/Bi0s/assets/69642777/e61f7b0c-53d6-4587-a972-8b3f72081a58)


## code

```cpp
void setup() {
  pinMode(11, OUTPUT);
  pinMode(12, OUTPUT);
  pinMode(13, OUTPUT);
  Serial.begin(9600);
}

void loop() 
{
  int sel=5;
  digitalWrite(11,bitRead(sel,0));
  digitalWrite(12,bitRead(sel,1));
  digitalWrite(13,bitRead(sel,2));

}
```

## Explanation

- 8:1 *mux* using 2:1 *mux* and selectline is controlled by arduino.  
- The inputs for the *mux* is given according to **Full Adder** which is ***sum and carry***.  
- The ***Sum*** output is displayed by the **<span style="color: red;">red led</span>** and ***carry*** output is displayed by the  **<span style="color: green;">green led</span>**.  
- The ***select lines*** are connected to arduino **Digital pins(<span style="color: cyan;">11,12,13</span>).**
- An integer variable <code>sel</code> and it stores decimal value which is later used as select line.  
```
| decimal | binary |  
| ------- | ------ |  
| 0       | 000    |
| 1       | 001    |  
| 2       | 010    |
| 3       | 011    |  
| 4       | 100    |
| 5       | 101    |  
| 6       | 110    |
| 7       | 111    | 
```

- <code>bitRead(x,n)</code> where ***x*** is the **sel** and ***n*** is the **binary bit position**.
- bitRead used to read the binary value of the given decimal and that is used as a select line   
for example: if the ***sel*** is given 5 then the binary (101) value of 0th position is assigined to Digital pin 11 which is S0.

```
S0-11-1
S1-12-0
S2-13-1
```

## Challenges faced

- While connecting the inputs for the mux.  

## Resources used
