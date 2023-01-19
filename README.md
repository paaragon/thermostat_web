# NODEMCU THERMOSTAT

This is an IOT project about a thermostat connected to wifi. Is based on the ESP8266 microcontroller and it has (optionally) two stations.

### Main station

The main station has a thermometer and a relay connected to the heater. It opens or close the relay based on the temperature measured by the thermometer and the temperature setted by the user. The relevant information is shown in a 16x2 LCD display. In order to set the temperature and control other options, the main station has four buttons. From left to right:

    1. Switch between local and remote mode (explains below).
    2. Turn on the screen (it turns off based on a timeout).
    3. Decrease the setted temperature
    4. Increase the setted temperature

### Satelite station

This station only has a thermometer and the microcrontroller. It sends the measures to the MQTT broker and if the main station is in "remote mode" that will be the temperature setted to control the heater

## Architecture diagram

![Diagram preview](./thermostat.png)

The diagram above shows all the components of the system and the connections between them.

The main and the satellite station communicates each other via the MQTT broker. Meanwhile, a python process is listening the MQTT topics in order to collect the information and stores it into the database.

The main station is prepared to change some parameters based on what it receives from the MQTT Broker. An HTTP API is provided by the `http_to_mqtt` application in order to remotely modify the setted temperature and mode of the main station.

The Grafana panels show relevant information to monitor