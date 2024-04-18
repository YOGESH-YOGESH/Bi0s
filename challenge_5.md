# Challenge 5

## code

```cpp
const int key = 5;

void setup() 
{
  Serial.begin(9600);
}

void loop() 
{
while (!Serial.available()) 
  {
    delay(10);
  }
  String encoded = Serial.readString();
  
  String decoded = caesarCipher (encoded, key);
  
  Serial.print("Original encoded: ");
  Serial.println (encoded);
  Serial.print("Encrypted encoded: ");
  Serial.println(decoded);
  delay(1000);
}

String caesarCipher(String encoded, int key) 
{
  String answer = "";
    for (int i = 0; i < encoded.length(); i++) 
    {
        if (isupper (encoded[i]))
          answer += char(int(encoded[i] + key - 65) % 26 + 65);
        else if(islower(encoded[i]))
          answer += char(int(encoded[i] + key - 97) % 26 + 97);
        else
          answer += encoded[i];
    }
  return answer;
}
```
## Explanation

### Caesar Cipher

Caesar Cipher is *monoalphabetic substitution Cipher*, where each letter is replaced by another letter which is little further in the same alphabetic.

---

- The shift is done here using a constant integer variable '**Key**'.

- The input is taken from the user via Serial monitor and stored as a string

- In the code the string is accessed one by one using a *for* loop and it checks whether it is Upper case or Lower case and according to that Operations are done, If that is a special character or a numeric values then it will skip and goes to next.

## Challenges faced 

## Resources used