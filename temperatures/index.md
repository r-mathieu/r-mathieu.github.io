# Temperatures


https://www.codingame.com/ide/puzzle/temperatures

#### **Goal**
We have to analyze records of temperature to find the closest to zero.

#### **Rules**
Write a program that prints the temperature closest to 0 among input data. If two numbers are equally close to zero, positive integer has to be considered closest to zero (for instance, if the temperatures are -5 and 5, then display 5).

#### **Solution**

```c++
#include <iostream>

using namespace std;

int main()
{
    int totalTemperatures; // the number of temperatures to analyse
    cin >> totalTemperatures; cin.ignore();

    int closestTemperature = 0;
    cin >> closestTemperature; cin.ignore();
    for (int index = 1; index < totalTemperatures; index++)
    {
        int temperature; // a temperature expressed as an integer ranging from -273 to 5526
        cin >> temperature; cin.ignore();

        if (abs(temperature) < abs(closestTemperature) || (temperature == -closestTemperature && temperature > 0))
        {
            closestTemperature = temperature;
        }
    }

    cout << closestTemperature << endl;
}
```
