# Mars Lander - Ep.1


https://www.codingame.com/ide/puzzle/mars-lander-episode-1

#### **Goal**

The goal for this program is to safely land the "Mars Lander" shuttle.

#### **Solution**
The solution can be easily found if you read all the statement and with only this so I'll skip all the informations.

**"vertical speed must be limited ( ≤ 40m/s in absolute value)"**.

```c++

#include <iostream>

using namespace std;

int main()
{
    int totalSurfacePoint; // the number of points used to draw the surface of Mars.
    cin >> totalSurfacePoint; cin.ignore();
    for (int index = 0; index < totalSurfacePoint; index++)
    {
        int landX; // X coordinate of a surface point. (0 to 6999)
        int landY; // Y coordinate of a surface point. By linking all the points together in a sequential fashion, you form the surface of Mars.
        cin >> landX >> landY; cin.ignore();
    }

    // game loop
    for(;;)
    {
        int X;
        int Y;
        int hSpeed; // the horizontal speed (in m/s), can be negative.
        int vSpeed; // the vertical speed (in m/s), can be negative.
        int fuel; // the quantity of remaining fuel in liters.
        int rotate; // the rotation angle in degrees (-90 to 90).
        int power; // the thrust power (0 to 4).
        cin >> X >> Y >> hSpeed >> vSpeed >> fuel >> rotate >> power; cin.ignore();

        int rotatePower = 0;
        int thrustPower = vSpeed <= -40 ? 4 : 0;
       cout << rotatePower << " "<< thrustPower << endl;
    }
}
```

