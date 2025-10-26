# Set Transmission (TX) Power

## Security-relevance

Security-assessment tools such as Blue2thprinting[1] or WHAD [2] may require making active connections to devices under test (DUT) in the wild. However, the DUT may be far away from the tester, and therefore may receive the connection attempts or packets within a connection with low signal strength. Therefore it is desirable for security-assessment tools to run on chips which have the ability to maximize the TX power, so that the DUT has a better chance of receiving packets from the tester.

[1] [Blue2thprinting (blue-\[tooth)-printing\]: answering the question of 'WTF am I even looking at?!'](https://darkmentor.com/bt.html#Blue2thprinting%20(blue-%5Btooth)-printing%5D%3A%20answering%20the%20question%20of%20'WTF%20am%20I%20even%20looking%20at%3F!':%5B%5BBlue2thprinting%20(blue-%5Btooth)-printing%5D%3A%20answering%20the%20question%20of%20'WTF%20am%20I%20even%20looking%20at%3F!'%5D%5D%20%5B%5BBluetooth%20Security%20Timeline%5D%5D%20%24%3A%2FTagManager) by Xeno Kovah  
[2] [One for all and all for WHAD: wireless shenanigans made easy!](https://darkmentor.com/bt.html#One%20for%20all%20and%20all%20for%20WHAD%3A%20wireless%20shenanigans%20made%20easy!) by Damien Caquile & Romain Cayre

## Vendors with VSC present

* [Silicon Labs](../vendor/SiliconLabs.md)
* [Texas Instruments](../vendor/TexasInstruments.md)