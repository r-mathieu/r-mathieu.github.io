# Horse Racing Duals


https://www.codingame.com/ide/puzzle/horse-racing-duals

#### **Goal**
Write a program which, using a given number of strengths, identifies the two closest strengths and shows their difference with an integer ( $ \eqslantgtr $ 0).

#### **Solution**
```c++

#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int main()
{
    int totalHorses;
    cin >> totalHorses; cin.ignore();

    //Get all value
    vector<int> allHorses(totalHorses);
    for(int index = 0; index < totalHorses; index++)
    {
        int currentHorse;
        cin >> currentHorse; cin.ignore();
        allHorses[index] = currentHorse;
    }

    //Sort value (default comparison, greater)
    sort(allHorses.begin(), allHorses.end());

    //Found smallest difference
    int smallestDiff = numeric_limits<int>::max();
    for(int index = 1; index < totalHorses; index++)
    {
        int diff = abs(allHorses[index - 1] - allHorses[index]);
        if(diff < smallestDiff)
        {
            smallestDiff = diff;
        }
    }

    cout << smallestDiff << endl;
}

```
