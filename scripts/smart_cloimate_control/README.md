# 🚗 Smart Car Climate Control Script

This script automatically adjusts your car’s climate control based on live weather conditions.  
It is designed for Hyundai / Kia vehicles with the Kia UVO / Hyundai Bluelink integration in Home Assistant.

## 🌡️ What It Does
- Reads outdoor conditions (temperature, humidex, dew point, humidity, UV, cloud cover, precipitation, visibility, wind, fog risk, day/night).  
- Calculates **optimal settings** for:
  - Cabin temperature (17–27 °C)
  - Duration (1–10 minutes)
  - Defrost (on in fog, snow, ice, or night fog)
  - Heating level (0–4)
  - Driver seat heater (0, 6, 7, 8)
  - Passenger seat heater (0, optional on very cold days)

- Applies overrides for **snow and ice** (max defrost, heating, full duration).  
- Differentiates **day vs night** (less aggressive cooling at night, stronger defrost in fog).  
- Sends a persistent notification with chosen settings before starting climate.  

## 🛠️ Requirements
- **PirateWeather** integration (temperature, dew point, humidity, UV, cloud, precip, visibility, wind, pressure)  
- **Environment Canada** (Montreal Humidex sensor, for feels-like)  
- **Sun integration** (for `is_day`)  
- **Kia UVO / Hyundai Bluelink integration** (for `kia_uvo.start_climate`)  
- *(Optional)* Template `fog_status` sensor if you want it visible on your dashboard
