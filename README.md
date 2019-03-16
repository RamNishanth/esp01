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


![image](https://user-images.githubusercontent.com/48613162/54474063-2b999580-4806-11e9-84a8-ec5297e5578d.png)


#                                        Getting Arduino UNO Ready for Programming ESP8266
In order to Program ESP8266 Module, we need to connect it to a computer. Since Serial Communication is the only available communication on the ESP8266 ESP-01 Module, we need an USB to Serial Adapter like an FTDI, CH340 or FT232RL.

If you do not have a dedicated USB to Serial Adapter, do not worry. The Arduino UNO has an on-board USB to Serial Adapter (which is used to program the Arduino). We are going to use this for programming the ESP8266.

We will be using the TX and RX Pins of the Arduino to connect to the ESP8266 Module and in order to make sure that Arduino isn’t using those pins, we can upload a bare minimum sketch to Arduino.

NOTE: Bare minimum sketch consists of just the setup and loop functions without any data in them.

In my case, I have an extra Arduino UNO Board with a non-functioning ATmega328p IC. So, I removed the Microcontroller IC from the Arduino UNO and started using it as an USB to Serial Converter.  
Circuit Design for Programming ESP8266 using Arduino
You have already seen the required components and the circuit diagram of the project. Now, let us try to understand the design of the circuit.

First and foremost, the ESP8266 Module works on 3.3V Power Supply and anything greater than that, like 5V for example, will kill the SoC. So, the VCC Pin and CH_PD Pin of ESP8266 ESP-01 Module are connected to a 3.3V Supply.

Next important thing to remember is that the ESP8266 WiFi Module has two modes of operation: Programming Mode and Normal Mode.

**In Programming Mode, you can upload the program or firmware to the ESP8266 Module and in Normal Mode, the uploaded program or firmware will run normally.**

**In order to enable the Programming Mode, the GPIO0 pin must be connected to GND. In the circuit diagram, I’ve connected a SPDT switch to the GPIO0 pin. Toggling the lever of SPDT will switch the ESP8266 between Programming mode (GPIO0 is connected to GND) and normal mode (GPIO0 acts as a GPIO Pin).**   

Also, the RST (Reset) will play an important role in enabling Programming Mode. The RST pin is an active LOW pin and hence, it is connected to GND through a Push Button. So, whenever the button is pressed, the ESP8266 Module will reset.

Finally the GPIO2 pin is connected to an LED to test the working of the program. All the necessary connections for enabling the Programming Mode in ESP8266 are mentioned below.
                ```
                    VCC – – > 3.3V
                    GND – – > GND
                    CH_PD – – > 3.3V
                    RST – – > Normally Open; GND to Reset
                    GPIO0 – – > GND
                    TX – – > TX of Arduino
                    RX – – > RX of Arduino (through level converter) ``` 

Working of ESP8266 Arduino Interface
Make sure that all the above mentioned connections are properly made. After connecting and configuring the ESP8266 in Programming Mode (GPIO0 is connected to GND), connect the Arduino to the system.

Once the ESP8266 Module is powered ON, Push the RST button and open the Arduino IDE. In the Board options (Tools –> Board), select the “Generic ESP8266” Board. Select the appropriate port number in the IDE.
                            

  ![image](https://user-images.githubusercontent.com/48613162/54473950-bda09e80-4804-11e9-8321-7d5c42a1b41e.png)

  
# SOURCE CODE
```
#define L1 0
#define L2 1
#define L3 2
#define L4 3
``` 
  #define used as macros , it doesn't take memory  
```void setup()
{
  pinMode(L1, OUTPUT);
  pinMode(L2, OUTPUT);
  pinMode(L3, OUTPUT);
  pinMode(L4, OUTPUT);
  
}
```

set GPIO pin as output

```void loop() 
{
    digitalWrite(L1, HIGH);
    digitalWrite(L2, HIGH);
    digitalWrite(L3, HIGH);
   digitalWrite(L4, HIGH);
  delay(1000);
  digitalWrite(L1, LOW);
    digitalWrite(L2, LOW);
    digitalWrite(L3, LOW);
   digitalWrite(L4, LOW);

  delay(1000);
}
 ``` 
 
  
  
  ### NOTE: DONT CONNECT LOADS ON GPIO , BEFORE FLASH YOUR CODE , OTHERWISE ESP01 WILL NOT WORK
  
  ### IN PROGRAMMING MODE MAKE GPIO 0 AS GROUND  , OTHERWISE ERROR WILL OCCUR
  
  
  
