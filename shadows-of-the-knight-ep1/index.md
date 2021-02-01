# Shadows of the Knight - Ep.1


https://www.codingame.com/ide/puzzle/shadows-of-the-knight-episode-1

#### **Goal**
Batman will look for the hostages on a given building by jumping from one window to another using his grapnel gun. Batman's goal is to jump to the window where the hostages are located in order to disarm the bombs. Unfortunately he has a limited number of jumps before the bombs go off...

#### **Rules**
Before each jump, the heat-signature device will provide Batman with the direction of the bombs based on Batman current position:
- U (Up)
- UR (Up-Right)
- R (Right)
- DR (Down-Right)
- D (Down)
- DL (Down-Left)
- L (Left)
- UL (Up-Left)

Your mission is to program the device so that it indicates the location of the next window Batman should jump to in order to reach the bombs' room as soon as possible.

Buildings are represented as a rectangular array of windows, the window in the top left corner of the building is at index (0,0).

#### **Solution**

```c++
#include <iostream>
#include <string>

using namespace std;

struct Point
{
    int X{ 0 };
    int Y{ 0 };

    Point() = default;
    Point(int _x, int _y)
        :X(_x), Y(_y)
    {}

    bool operator==(const Point& _value) const { return X == _value.X && Y == _value.Y; }
};

class Batman
{
    private:
        Point m_CurrentPosition;
        Point m_MinPoint;
        Point m_MaxPoint;

        int m_BuildingWidth { 0 };
        int m_BuildingHeight { 0 };

        int m_NumberTurn{ 0 };

    public:
        Batman() = default;

    public:
        void AnalyzeSituation()
        {
            cin >> m_BuildingWidth >> m_BuildingHeight; cin.ignore();

            cin >> m_NumberTurn; cin.ignore();

            cin >> m_CurrentPosition.X >> m_CurrentPosition.Y; cin.ignore();

            m_MaxPoint = Point(m_BuildingWidth, m_BuildingHeight);
        }

        void FoundBomb()
        {
            string bombDirection; // the direction of the bombs from batman's current location (U, UR, R, DR, D, DL, L or UL)
            cin >> bombDirection; cin.ignore();

            if(bombDirection.find('U') != string::npos)
            {
                m_MaxPoint.Y = m_CurrentPosition.Y - 1;
            }
            else if(bombDirection.find('D') != string::npos)
            {
                m_MinPoint.Y = m_CurrentPosition.Y + 1;
            }

            if(bombDirection.find('L') != string::npos)
            {
                m_MaxPoint.X = m_CurrentPosition.X - 1;
            }
            else if(bombDirection.find('R') != string::npos)
            {
                m_MinPoint.X = m_CurrentPosition.X + 1;
            }

            m_CurrentPosition.X = (m_MaxPoint.X + m_MinPoint.X) / 2;
            m_CurrentPosition.Y = (m_MaxPoint.Y + m_MinPoint.Y) / 2;

            cout << m_CurrentPosition.X << " " << m_CurrentPosition.Y << endl;
            cerr << m_MinPoint.X << " " << m_MinPoint.Y << endl;
            cerr << m_MaxPoint.X << " " << m_MaxPoint.Y << endl;

            m_NumberTurn--;
        }

        bool CanSearch() const { return m_NumberTurn > 0;}
};

int main()
{
    Batman* batman = new Batman();
    batman->AnalyzeSituation();

    // game loop
    for(;batman->CanSearch();)
    {
        batman->FoundBomb();
    }

    delete batman;
}
```
