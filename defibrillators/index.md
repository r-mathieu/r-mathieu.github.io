# Defibrillators


https://www.codingame.com/ide/puzzle/defibrillators

#### **Goal**

Based on the data we provide in the tests, write a program that will allow users to find the defibrillator nearest to their location using their mobile phone.

#### **Rules**

The input data you require for your program is provided in text format. This data is comprised of lines, each of which represents a defibrillator.
Each defibrillator is represented by the following fields:
- A number identifying the defibrillator
- Name
- Address
- Contact Phone number
- Longitude (degrees)
- Latitude (degrees)

These fields are separated by a semicolon.
The distance **d** between two points **A** and **B** will be calculated using the following formula:

$$ x = (longitudeB - longitudeA) * cos \genfrac ( ) {1pt}{0}{latitudeB - latitudeA}{2}  $$
$$ y = latitudeB - latitudeA $$
$$ d = \sqrt{x^2 + y^2} * 6371 $$

The program will display the name of the defibrillator located the closest to the user’s position.

#### **Solution**

```c++

#include <iostream>
#include <string>
#include <vector>
#include <algorithm>
#include <cstring>
#include <sstream>
#include <cmath>

using namespace std;

namespace Helper
{
    // Parses a string to double and replacing ',' by '.'
    // Return zero (0.0) if can't
    double StringToDouble(const string& _string)
    {
        char* cstr = new char[_string.length() + 1];
        strcpy(cstr, _string.c_str());

        for(char *iter = cstr; *iter != '\0'; iter++)
        {
            if (*iter == ',')
            {
                *iter = '.';
            }
        }

        return atof(cstr);
    }

    // Split a string with a delimiter
    // Return a vector<string>
    vector<string> Split(const string& _string, char _delimiter)
    {
        vector<string> splitResult;
        string split;
        istringstream splitStream(_string);

        while (getline(splitStream, split, _delimiter))
        {
            splitResult.push_back(split);
        }
        return splitResult;
    }
}

struct Defibrillator
{
public:
    string location;
    double longitude{ 0.0 };
    double latitude{ 0.0 };

    Defibrillator(const string& _message)
    {
        vector<string> splittedMessage = Helper::Split(_message, ';');
        //Add a assert if length is different to 6

        location = splittedMessage[1];
        longitude = Helper::StringToDouble(splittedMessage[4]);
        latitude = Helper::StringToDouble(splittedMessage[5]);
    }
};

int main()
{
    double userLongitude{ 0.0 };
    double userLatitude{ 0.0 };;
    {
        string longitudeString;
        string latitudeString;
        cin >> longitudeString; cin.ignore();
        cin >> latitudeString; cin.ignore();

        userLongitude = Helper::StringToDouble(longitudeString);
        userLatitude = Helper::StringToDouble(latitudeString);
    }

    int totalDefibrillator;
    cin >> totalDefibrillator; cin.ignore();

    vector<Defibrillator> allDefibrillators;
    allDefibrillators.reserve(totalDefibrillator);

    ////Get all defibrillator
    for (int index = 0; index < totalDefibrillator; index++)
    {
        string defibrillator;
        getline(cin, defibrillator);

        allDefibrillators.push_back(Defibrillator(defibrillator));
    }

    ////Get nearest defibrillator
    double sqrNearestDist = numeric_limits<double>::max();
    string nearestLocation;
    for(Defibrillator& defibrillator : allDefibrillators)
    {
        double x = (defibrillator.longitude - userLongitude) * cos((userLongitude + defibrillator.longitude) / 2.0);
        double y = defibrillator.latitude - userLatitude;
        double sqrtDist = x*x + y*y;

        if(sqrtDist < sqrNearestDist)
        {
            sqrNearestDist = sqrtDist;
            nearestLocation = defibrillator.location;
        }
    }

    cout << nearestLocation << endl;
}
```
