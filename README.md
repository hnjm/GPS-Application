### Screenshot
![](https://raw.githubusercontent.com/GregBarber/GPS-Application/master/GPS-Application/Screenshots/DisplayFilteredData.jpg)

Demonstrates track data that has been loaded in (shown as blue points), with a separate track that has been created using a time and distance filter (shown as orange points).  The general path has been preserved while unnecessary points have been filtered out.

### Motivation.
From my travels I have an enormous amount of GPS data logged.  I use this data to tag photos with location information.  Originally I had been using existing tagging software but found it lacking in several areas.  First, it was unable to account for noise in the GPS signal.  As a result, photos taken in the same location would often be tagged with very different locations.  Second, it was impossible to handle situations where a GPS signal was lost temporarily.  The photo would receive no location tag as a result.

Unable to find existing software to handle my needs, I decided to make my own.

### Requirements
The program needs to be able to read and write the GPS data which comes in NMEA format.  Reading is obvious, since it is required to begin manipulating the data.  Writing is necessary because I want to be able to reuse tracks after they have been filtered.  Also, I want the ability to merge tracks, especially after filtering out a lot unnecessary data.  As an example it would be nice to export a single GPS track that covers all my travels as a single, but manageable in size and number of points, file.

Second, the program needs to display the track information on a map using different markers for each data set.

Third, filters need to be implemented that reduce noise as well as remove unnecessary points based on time and/or distance.  My research and experience lead me to decide that a Kalman filter is the best method for reducing noise.  A nice feature to have would be having sliders that control the input to the filters, and have the track data update immediately on the map to visualize the effect.

In the long run it would be nice to have the program handle tagging photos directly, rather than exporting filtered tracks to another program for tagging.

### Status
Currently the program is able to import and export valid NMEA formatted GPS data similar to the example below

NMEA Formatted GPS Data:

```
$GPRMC,030735.222,A,2741.2424,N,08643.9042,E,0.38,8.03,300413,,,A*6D
$GPVTG,8.03,T,,M,0.38,N,0.7,K,N*05
$GPGGA,030740.222,2741.2453,N,08643.9058,E,1,03,7.5,2846.6,M,-37.4,M,,0000*41
$GPGSA,A,2,22,14,11,,,,,,,,,,7.6,7.5,1.0*34
$GPGSV,3,1,12,22,69,052,39,14,57,348,41,11,14,305,33,31,46,202,25*73
$GPGSV,3,2,12,18,43,101,24,25,22,102,,21,14,164,,12,13,069,*7C
$GPGSV,3,3,12,19,07,263,,24,04,038,,01,03,323,,06,01,226,*7A
```

I have written a program for displaying the tracks that used an open source Widows form control [GMaps .NET](https://greatmaps.codeplex.com/).  From this program the user can load and visualize the track data choosing between 37 different icons.  Currently only the time and distance filter has been completed.  All existing features have unit tests as part of the code.  The Kalman filter is still in development.

### Sample Usage
Shown is a simple demonstration of how the program is used.

In this demo, a GPS track of a flight into Kathmandu airport is loaded.  On approach the plane is seen to circle once around before landing.  A filter is applied using time and distance parameters to remove unnecessary points from the GPS track.  Only a few points are saved during the flight, while more points remain during surface transportation winding through slow moving Kathmandu traffic.

![](https://raw.githubusercontent.com/GregBarber/GPS-Application/master/GPS-Application/Screenshots/InitialLogLoaded.jpg)
After loading the unfiltered track.

***

![](https://raw.githubusercontent.com/GregBarber/GPS-Application/master/GPS-Application/Screenshots/ApplySimpleFilter.jpg)
Applying a simple filter.

***

![](https://raw.githubusercontent.com/GregBarber/GPS-Application/master/GPS-Application/Screenshots/DisplayFilteredData.jpg)
The amount of track data has been reduced, as shown by the orange points, while still preserving the overall path followed.
