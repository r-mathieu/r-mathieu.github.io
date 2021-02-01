# Chuck Norris


https://www.codingame.com/ide/puzzle/chuck-norris

#### **Goal**

Write a program that takes an incoming message as input and displays as output the message encoded using *Chuck Norris’ method*.

#### **Rules**
The input message consists of ASCII characters (7-bit).
The encoded output message consists of blocks of 0.
A block is separated from another block by a space.
Two consecutive blocks are used to produce a series of same value bits (only1 or0 values):
- First block: it is always 0 or 00. If it is 0, then the series contains 1, if not, it contains 0
- Second block: the number of 0 in this block is the number of bits in the series



#### **Solution**
```c++

#include <iostream>
#include <string>
#include <bitset>

using namespace std;

int main()
{
    string message;
    getline(cin, message);

    string encodedMessage = "";
    char previousValue = 'a';
    for(char& charMessage : message)
    {
        string binaryMessage = bitset<7>(charMessage).to_string();
        
        for(int index = 0; index < binaryMessage.length(); index++)
        {
            const char& value = binaryMessage[index];

            if(value == previousValue)
            {
                encodedMessage += '0';
            }
            else
            {
                string block = encodedMessage.length() > 0 ? " " : "";
                block.insert(block.length(), value == '1' ? "0 " : "00 ");

                encodedMessage.insert(encodedMessage.length(), block);
                index--;
            }

            previousValue = value;
        }
    }

    cout << encodedMessage << endl;
}

```
