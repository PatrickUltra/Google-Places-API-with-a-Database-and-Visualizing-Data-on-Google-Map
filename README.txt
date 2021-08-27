Utilization of the Google Places API in conjunction with a database and visualization of data on a Google Map

In this project, we're going to use the Google geocoding API to clean up some user-entered geographic coordinates of institution names before plotting them on a Google Map.

Note: Because Windows has problems showing UTF-8 characters in the console, you may need to type the following command before running this code for each command window you open:

chcp 65001 

http://stackoverflow.com/questions/388490/unicode-characters-in-windows-command-line-how


You should install the SQLite browser in order to view and alter databases from the following locations:

http://sqlitebrowser.org/

The first issue to address is the rate limit on the Google geocoding API, which is set to a predetermined number of requests per day.
As a result, if you have a large amount of data, the lookup process may need to be stopped and restarted numerous times. As a result, we divide the task into two sections.

We begin by reading our input data from the file (where.data) one line at a time, obtaining the geocoded response and storing it in a database (geodata.sqlite).
We simply check to verify if we already have the data for that particular line of input before calling the geocoding API.

At any moment, you can restart the process by deleting the file geodata.sqlite.

Execute the geoload.py script. This application will read the lines in where.data and check to see if they are already in the database. If they are not, it will contact the geocoding API to retrieve and store the data for the place.

As of December 2016, Google's geocoding APIs underwent significant changes.
They consolidated some of the Geocoding API's capabilities into the Places API. Additionally, an API key is required for any Google Geo-related APIs. To complete this assignment without a Google account, an API key, or from a country that restricts access to Google, you can get a subset of that data at:

http://py4e-data.dr-chuck.net/json

To use this, simply leave the api key variable in geoload.py set to False.

This URL contains only a fraction of the data, but it does not have a rate limit, making it ideal for testing.

If you'd want to experiment with this using the API key, follow the instructions at:

https://developers.google.com/maps/documentation/geocoding/intro

and populate the code with the API key.

Here is a sample run after some data has been entered into the database:

python3 geoload.py python3 geoload.py python3 geoload.py
geoload.py

Due to the fact that the first five places are already in the database, they are omitted. The program scans until it discovers un-retrieved places and then begins recovering them.

The geoload.py process can be terminated at any moment, and there is a counter that can be used to limit the amount of requests to the geocoding API made during each run.

Once some data has been put into geodata.sqlite, the (geodump.py) application can be used to view the data. This software reads the database and writes the location, latitude, and longitude in the form of executable JavaScript code to the tile file (where.js).

The geodump.py program is executed as follows:

Python3 geodump.py FOR WINDOWS
Geodump.py

This is a JavaScript collection of collections. JavaScript list constants have a syntax that is extremely similar to Python, so you should be comfortable with it.

To view the locations, simply open where.html in a browser. Hover over each map point to see the location supplied by the geocoding API for the user-entered data. If you are unable to view any data when you open the where.html page, you may wish to check your browser's JavaScript or developer console.
