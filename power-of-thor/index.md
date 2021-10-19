# Power of thor


https://www.codingame.com/ide/puzzle/power-of-thor-episode-1

#### **Goal**
The program must allow Thor to reach the light of power.

#### **Rules**
Thor moves on a map which is 40 wide by 18 high. The coordinates (X and Y) start at the top left.

Once the program starts, there's the following input:
- the variable lightX: the X position of the light of power that Thor must reach.
- the variable lightY: the Y position of the light of power that Thor must reach.
- the variable initialTX: the starting X position of Thor.
- the variable initialTY: the starting Y position of Thor.

At the end of the game turn, you must output the direction in which you want Thor to go among:
- N (North)
- NE (North-East)
- E (East)
- SE (South-East)
- S (South)
- SW (South-West)
- W (West)
- NW (North-West)

#### **Solution**

```c++

#include <iostream>
#include <string>

using namespace std;

int main()
{
    int lightX; // the X position of the light of power
    int lightY; // the Y position of the light of power
    int initialTX; // Thor's starting X position
    int initialTY; // Thor's starting Y position
    cin >> lightX >> lightY >> initialTX >> initialTY; cin.ignore();

    int currentTX = initialTX;
    int currentTY = initialTY;

    // game loop
    for(;;)
    {
        int remainingTurns; // The remaining amount of turns Thor can move. Do not remove this line.
        cin >> remainingTurns;
        cin.ignore();

        string XResult = "";
        string YResult = "";

        //LATERAL MOVEMENT
        if(currentTX > lightX)
        {
            XResult = 'W';
            currentTX--;
        }
        else if(currentTX < lightX)
        {
            XResult = 'E';
            currentTX++;
        }
        
        //VERTICAL MOVEMENT
        if(currentTY > lightY)
        {
            YResult = 'N';
            currentTY--;
        }
        else if(currentTY < lightY)
        {
            YResult = 'S';
            currentTY++;
        }

        cout << YResult << XResult << endl;
    }
}
```
