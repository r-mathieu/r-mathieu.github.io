# Network Cabling


https://www.codingame.com/ide/puzzle/network-cabling

#### **Goal**
An internet operator plans to connect a business park to the optical fiber network. The area to be covered is large and the operator is asking you to write a program that will calculate the minimum length of optical fiber cable required to connect all buildings.

#### **Rules**
For the implementation of the works, the operator has technical constraints whereby it is forced to proceed in the following manner:
A main cable will cross through the park from the West to the East (from the position x of the most westerly building to the position x of the most easterly building).

For each building, a dedicated cable will connect from the building to the main cable by a minimal path (North or South), as shown in the following example:

{{<image src="https://www.codingame.com/fileservlet?id=11638050532">}}

The minimum length will therefore depend on the position of the main cable.

#### **Solution**

```c++

#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int main()
{
    int totalHouse;
    cin >> totalHouse; cin.ignore();

    int minPosX = numeric_limits<int>::max();
    int maxPosX = numeric_limits<int>::min();
    
    vector<pair<int, int>> allHousePosition(totalHouse);
    for (int index = 0; index < totalHouse; index++)
    {
        int X;
        int Y;
        cin >> X >> Y; cin.ignore();

        if (X < minPosX)
        {
            minPosX = X;
        }

        if (X > maxPosX)
        {
            maxPosX = X;
        }
        
        allHousePosition[index] = pair<int, int>( X, Y);
    }

    long int totalLength = maxPosX - minPosX; //Init value with the length of the main cable

    // Calculate the median y position
    auto comparison = [](const pair<int, int>& _firstHouse, const pair<int, int>& _secondHouse)
                        {
                            return _firstHouse.second < _secondHouse.second;
                        };
                        
    sort(allHousePosition.begin(), allHousePosition.end(), comparison);

    int mainCableY = 0;
    if (allHousePosition.size() % 2)
    {
        mainCableY = allHousePosition[allHousePosition.size() / 2].second;
    }
    else
    {
        mainCableY = (allHousePosition[(allHousePosition.size() / 2)-1].second + allHousePosition[allHousePosition.size() / 2].second) / 2;
    }

    // Calculate the total length of the cables
    for (pair<int, int>& housePosition : allHousePosition)
    {
        totalLength += abs(mainCableY - housePosition.second);
    }
    
    cout << totalLength << endl;
}
```
