# kichu
from os import write
import requests
from datetime import datetime

api_key = 'e41be5d25c7ba335590e66d2d871fe7a'  # API Key for WeatherAPI
location = input("Enter the city name: ")   # stores the city name for which the weather details will be fetched

complete_api_link = "https://api.openweathermap.org/data/2.5/weather?q="+location+"&appid="+api_key   # url using which we get the Details for the entered City
api_link = requests.get(complete_api_link)
api_data = api_link.json() # Weather details retrieved are saved as .json file

temp_city = ((api_data['main']['temp']) - 273.15)   # stores temperature of City in °C
weather_desc = api_data['weather'][0]['description']    # stores weather description
hmdt = api_data['main']['humidity']   # stores Humidity of the City
wind_spd = api_data['wind']['speed']    # stores Wind Speed
date_time = datetime.now().strftime("%d %b %Y | %I:%M:%S %p")   # stores the Date & Time when the Weather Data was fetched

temp_city="{:.2f}".format(temp_city)    # rounds the temperature of city upto 2 decimal places

f=open("Weather Log.txt","a")   # opens/creates a file names "Weather Log" to stores Weather Details in Append Mode

t = ("\n\n-------------------------------------------------------------\n") 
print(t)
f.write(t)    
t = ("Weather Stats for - {}  || {}\n".format(location.upper(), date_time))     # Location and Date & Time when the Details were recorded
print(t)
f.write(t)
t = ("-------------------------------------------------------------\n")
print(t)
f.write(t)
t = ("Current temperature is: "+temp_city+" °C\n")      # Temperature of the City
print(t)
f.write(t)
t = ("Current Weather desc  :"+weather_desc+"\n")     # Weather Description of the City
print(t)
f.write(t)
t = ("Current Humidity      :"+str(hmdt)+'%\n')     # Humidity of the City
print(t)
f.write(t)
t = ("Current Wind Speed    :"+str(wind_spd)+'kmph\n')      # Wind Speed at City
print(t)
f.write(t)
f.close()     # closes the file "Weather Log.txt"
