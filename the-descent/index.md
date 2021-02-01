# The Descent


https://www.codingame.com/ide/puzzle/the-descent

#### **Goal**
Destroy the mountains before your starship collides with one of them. For that, shoot the highest mountain on your path.

#### **Rules**
At the start of each game turn, you are given the height of the 8 mountains from left to right.
By the end of the game turn, you must fire on the highest mountain by outputting its index (from 0 to 7).

Firing on a mountain will only destroy part of it, reducing its height. Your ship descends after each pass.  

#### **Solution**

```c++
#include <iostream>

using namespace std;

int main()
{
    int targetIndex = 0;

    // game loop
    for(;;)
    {
        int highestMountain = 0;
        for (int index = 0; index < 8; index++)
        {
            int mountainHeight;
            cin >> mountainHeight;
            cin.ignore();

            if(mountainHeight >= highestMountain)
            {
                targetIndex = index;
                highestMountain = mountainHeight;
            }

        }

        cout << targetIndex << endl;
    }
}
```
