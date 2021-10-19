# Mars Lander


https://www.codingame.com/ide/puzzle/mars-lander-episode-2

#### **Goal**
The goal for your program is to safely land the "Mars Lander" shuttle, the landing ship which contains the Opportunity rover. Mars Lander is guided by a program, and right now the failure rate for landing on the NASA simulator is unacceptable.

This puzzle is the second level of the "Mars Lander" trilogy. The controls are the same as the previous level but you must now control the angle in order to succeed.

#### **Rules**

Built as a game, the simulator puts Mars Lander on a limited zone of Mars sky.

{{<image src="https://www.codingame.com/fileservlet?id=2635325710601">}}

The zone is **7000m wide** and **3000m high**.
There is a unique area of flat ground on the surface of Mars, which is at least 1000 meters wide.

Every second, depending on the current flight parameters (location, speed, fuel ...), the program must provide the new desired tilt angle and thrust power of Mars Lander:

{{<image src="https://www.codingame.com/fileservlet?id=957023678862">}}

Angle goes from **-90° to 90°**. Thrust power goes from **0 to 4**.

The game simulates a free fall without atmosphere. Gravity on Mars is **3.711 m/s²**. For a thrust power of X, a push force equivalent to X m/s² is generated and X liters of fuel are consumed. As such, a thrust power of **4** in an almost vertical position is needed to compensate for the gravity on Mars.

For a landing to be successful, the ship must:
- land on flat ground
- land in a vertical position (tilt angle = 0°)
- vertical speed must be limited ( ≤ 40m/s in absolute value)
- horizontal speed must be limited ( ≤ 20m/s in absolute value)

#### **Solution**

```c++
#define _USE_MATH_DEFINES //GET PI VALUE

#include <iostream>
#include <string>
#include <vector>
#include <algorithm>
#include <utility>
#include <cmath>

using namespace std;

static constexpr int K_HSPEED_LIMIT = 20;
static constexpr int K_VSPEED_LIMIT= 40;
static constexpr float K_MARS_GRAVITY= 3.711f;

class MarsLander
{
public:
    pair<int, int> m_LandingZone;
    int m_WidthAreaLanding{ 0 };

    int m_X{ 0 };
    int m_Y{ 0 };
    int m_HSpeed{ 0 }; // the horizontal speed (in m/s), can be negative.
    int m_VSpeed{ 0 }; // the vertical speed (in m/s), can be negative.
    int m_Fuel{ 0 }; // the quantity of remaining fuel in liters.
    int m_Rotate{ 0 }; // the rotation angle in degrees (-90 to 90).
    int m_Power{ 0 }; // the thrust power (0 to 4).

public:
    MarsLander() = default;

public:
    void CheckInstruments()
    {
        cin >> m_X >> m_Y >> m_HSpeed >> m_VSpeed >> m_Fuel >> m_Rotate >> m_Power;
        cin.ignore();
    }

    bool IsLanded() const
    {
        return IsAlign() && m_LandingZone.second == m_Y;
    }

    void PerformLanding()
    {
        pair<int, int> result;

        if(IsAlign())
        {   
            //Too fast
            if(abs(m_HSpeed) > K_HSPEED_LIMIT / 2)
            {
                result.first = GetSlowingAngleValue();
                result.second = abs(result.first - m_Rotate) > 60 ? 2 : 4;
            }
             //Hover
            else
            {
                result.first = 0;
                result.second = m_VSpeed <= -K_VSPEED_LIMIT ? 4 : 2;
            }
        }
        else
        {
            //Too fast
            if(abs(m_HSpeed) > K_HSPEED_LIMIT * 3)
            {
                result.first = clamp(GetSlowingAngleValue(), -35, 35);
                result.second = (abs(result.first - m_Rotate) < 90 || abs(m_Rotate) > 35) ? 4 : 1; //avoid big acceleration in wrong direction
            }
            //Too slow
            else if (abs(m_HSpeed) < K_HSPEED_LIMIT * 2)
            {
                result.first = GetAlignmentValue();
                result.second = m_VSpeed < 0 ? 4 : 3;
            }
            //Hover
            else
            {
                result.second = m_VSpeed < 0 ? 4 : 0;
            }
        }

        cout << result.first << " " << result.second << endl;
    }

private:
    float GetSpeed() const{ return sqrt(m_HSpeed * m_HSpeed + m_VSpeed * m_VSpeed); }

    bool IsAlign() const { return m_X > m_LandingZone.first - (m_WidthAreaLanding / 3) && m_X < m_LandingZone.first + (m_WidthAreaLanding / 3); }

    int GetAlignmentValue() const
    {
        int angle = acos(K_MARS_GRAVITY / 4.0f) * (180.0f / M_PI);
        angle *= (m_X < m_LandingZone.first ? -1 : 1);
        return angle;
    }

    int GetSlowingAngleValue() const { return asin(m_HSpeed / GetSpeed()) * 180.0f / M_PI; }
};

class NASA
{
private:
    MarsLander* p_Ship{ nullptr };

public:
    NASA() = default;
    ~NASA()
    {
        delete p_Ship;
    }

public:
    MarsLander* LaunchLander()
    {
        p_Ship = new MarsLander();
        CalculateLandingZoneArea();
        return p_Ship;
    }

    void EndMission()
    {
        cerr << "Celebrate landing." << endl;
    }

private:
    void CalculateLandingZoneArea()
    {
        int totalSurfaces; // the number of points used to draw the surface of Mars.
        cin >> totalSurfaces; cin.ignore();

        pair<int, int> previousXYPoint;
        for (int index = 0; index < totalSurfaces; index++)
        {
            int landX; // X coordinate of a surface point. (0 to 6999)
            int landY; // Y coordinate of a surface point. By linking all the points together in a sequential fashion, you form the surface of Mars.
            cin >> landX >> landY; cin.ignore();

            if(previousXYPoint.second == landY)
            {
                p_Ship->m_LandingZone.first = (previousXYPoint.first + landX) / 2;
                p_Ship->m_LandingZone.second = landY;

                p_Ship->m_WidthAreaLanding = landX - previousXYPoint.first;

                //Don't break or it'll miss the order of the reading value
            }

            previousXYPoint.first = landX;
            previousXYPoint.second = landY;
        }

        cerr << p_Ship->m_LandingZone.first <<" , " << p_Ship->m_LandingZone.second << endl;
    }
};

int main()
{
    NASA* nasa = new NASA();
    MarsLander* ship = nasa->LaunchLander();
    
    //game loop
    for(;!ship->IsLanded();)
    {
        ship->CheckInstruments();

        ship->PerformLanding();
    }

    nasa->EndMission();
    delete nasa;
}
```
