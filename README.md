#                                         ARDUINO UNO  WITH GPIO WORKING CONCEPT
# Components
                                Arduino UNO  
                                ESP8266 ESP-01 
                                Connecting Wires 
                                Bread Board or  DOT board
                                Push Button
#                                          Connecting the ESP8266 to an Arduino
The steps you need to take are simple. This is written for the ESP8266-01 but you can find the pinout for other models easily and use the same pins. First we will connect the Arduino UNO to a breadboard:

1. Connect the Arduino’s 3v3 **(3.3V)**  on a breadboard. The ESP8266 works with 3.3V and not 5V, so this is necessary. If you want to connect other components that use 5V, you can connect the 5V output of the breadboard, just make sure you don’t connect the two.

2. Connect GND (ground) to breadboard.

3. Connect the RES or RESET pin to ground. When you ground the reset pin, the Arduino works as a dumb USB to serial connector, which is what we want to talk to the ESP8266.

4. Connect the RXD pin of the Arduino to the RX pin of the ESP8266 .

5. Connect the TXD pin of the Arduino to the TX pin of the ESP (green color in the picture). Usually, when we want two things to talk to each other over serial, we connect the TX pin of one to the RX of the other (send goes to receive and the opposite). Here we do not have the Arduino talk to the ESP8266 though, our computer is talking to it via the Arduino.

6. Connect the GND pin of the ESP to the blue line and the VCC pin to the red line.
Finally CH_PD goes to the red line, supposedly it will not work if you do not connect this.
#          ESP01
![image](https://user-images.githubusercontent.com/48613162/54473814-e031b800-4802-11e9-88c4-1e0f57c7978b.png)
#                                    Pin Description of ESP8266 ESP-01 Module
    VCC: It is the power pin through which 3.3V is supplied.
    GND: It is the ground pin.
    TX: This pin is used to transmit serial data to other devices.
    RX: The RX pin is used to receive serial data from other devices.
    RST: It is the Reset Pin and it is an active LOW Pin. (ESP8266 will reset if the RST pin receives LOW signal).
    CH_PD: This is the chip enable pin and it is an active HIGH Pin. It is usually connected to 3.3V.
    GPIO0: The GPIO0 (General Purpose I/O) Pin has dual functions – one for normal GPIO Operation and other for enabling the Programming     Mode of ESP8266.
    GPIO2: This is GPIO Pin.
IMPORTANT NOTE: The ESP8266 is not compatible with 5V and the ESP-01 Module does not have any voltage regulators on-board. Make sure that the power supply to the ESP8266 is 3.3V, preferably from a dedicated power supply rather than taking it from the 3.3V Pin of the Arduino.
  #  CIRCUIT DIAGRAM
  ![image](https://user-images.githubusercontent.com/48613162/54473880-b927b600-4803-11e9-9f2b-57999c40f4e2.png)
  #                                Getting Arduino IDE Ready for Programming ESP8266

ESP8266 WiFi Module can be programmed using Arduino IDE and in order to do that you need to make a few changes to the Arduino IDE. First, go to File –> Preferences in the Arduino IDE and in the Additional Boards Manager URLs Section, enter the following URL.
                            
                            http://arduino.esp8266.com/stable/package_esp8266com_index.json
                            
 NOTE: You can add many such URLs but they must be separated with commas.

Now, go to Tools –> Board –> Boards Manager and search for ESP8266 in the search field. Select the ESP8266 by ESP8266 Community and click on Install.          


                            

  
  
  
  
  
  
  
  
  
  
