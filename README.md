# Weather-Data-Compliation
Enter weather data about a region and complete various calculations
#include <iostream>
#include <cstring>
#include <iomanip>
using namespace std;

enum MONTHS {JANUARY, FEBRUARY, MARCH, APRIL, MAY, JUNE, JULY, AUGUST, SEPTEMBER, OCTOBER, NOVEMBER, DECEMBER};

//Structure with all required data
struct WeatherData
{
  string region_Name;
  double total_Rainfall;
  double high_Temperature;
  double low_Temperature;
  double average_Temperature;
};

int main() 
{
//Array to hold all stucture data for one year (12 months)
struct WeatherData monthsForStruct[12]; 

cout << "Enter region name: \n";
//This will be saved into the structure for the first element of the array. No other element will have an entry for the region name.
cin >>  monthsForStruct[0].region_Name;

//Collect data for each month
int index=0;
double cumrainfall=0;
double cumavgtemp=0;

for(index=JANUARY; index<=DECEMBER; index++)
{
  cout << "For month " << index <<": \n";
  cout<< "Enter total rainfall: \n";
  cin >> monthsForStruct[index].total_Rainfall;


  cout<< "Enter high temp: \n";
  cin >> monthsForStruct[index].high_Temperature;
  while (monthsForStruct[index].high_Temperature < -100 || monthsForStruct[index].high_Temperature > 150)
    {
    cout << "That temperature is very extreme! If you entered incorrectly, please input again. If not, please reconsider this destination: ";
    cin >> monthsForStruct[index].high_Temperature;
    }
  cout<< "Enter low temp: \n";
  cin >> monthsForStruct[index].low_Temperature;
  while (monthsForStruct[index].low_Temperature < -100 || monthsForStruct[index].low_Temperature > 150)
    {
    cout << "That temperature is very extreme! If you entered incorrectly, please input again. If not, please reconsider this destination: ";
    cin >> monthsForStruct[index].low_Temperature;
    }


  monthsForStruct[index].average_Temperature = (monthsForStruct[index].high_Temperature+monthsForStruct[index].low_Temperature)/2;
  cout << fixed << showpoint << setprecision(2) << "The average temp was: " << monthsForStruct[index].average_Temperature << endl;
  cout << "*****************************\n";

  cumrainfall += monthsForStruct[index].total_Rainfall;
  cumavgtemp += monthsForStruct[index].average_Temperature;

}
cout << "Data for " << monthsForStruct[0].region_Name <<endl;
cout << fixed << showpoint << setprecision(2) <<
"The average monthly rainfall was: " << cumrainfall/12 <<endl
<< "The total yearly rainfall was: " << cumrainfall <<endl
<< "The average monthly temp was: " << cumavgtemp/12 <<endl;

//Month with high temp
int temp_highmonth=0;
for(index=JANUARY; index<=DECEMBER; index++)
{
 if (monthsForStruct[index].high_Temperature > monthsForStruct[temp_highmonth].high_Temperature)
  temp_highmonth=index;
}
cout << "The month with the highest temperature was month " <<temp_highmonth<< " with a high temp of " << monthsForStruct[temp_highmonth].high_Temperature <<endl;


//Month with low temp
int temp_lowmonth=0;
for(index=JANUARY; index<=DECEMBER; index++)
{
 if (monthsForStruct[index].low_Temperature < monthsForStruct[temp_lowmonth].low_Temperature)
  temp_lowmonth=index;
}
cout << "The month with the loweest temperature was month " <<temp_lowmonth<< " with a low temp of " << monthsForStruct[temp_lowmonth].low_Temperature <<endl;

//Month with most rain
int temp_rainmonth=0;
for(index=JANUARY; index<=DECEMBER; index++)
{
 if (monthsForStruct[index].total_Rainfall > monthsForStruct[temp_rainmonth].total_Rainfall)
  temp_rainmonth=index;
}
cout << "The month with the most rain was month " <<temp_rainmonth<< " with rainfall totaling " << monthsForStruct[temp_rainmonth].total_Rainfall <<endl;

return 0;
}
