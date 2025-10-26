# Send arbitrary LLCP (Link Layer Control Protocol) packets

## Security-relevance

Security-assessment tools such as Blue2thprinting[1] or fuzzers like Sweyntooth[2] may require making active connections to devices under test (DUT) in the wild, and sending raw LLCP packets to perform their assessment. Official interfaces to send LLCP packets (for which there is no BT spec-defined method for them to be created by the host), allows security-assessment tools to perform their function without needing to resort to custom firmwares (which are a maintenance burden.)

[1] [Blue2thprinting (blue-\[tooth)-printing\]: answering the question of 'WTF am I even looking at?!'](https://darkmentor.com/bt.html#Blue2thprinting%20(blue-%5Btooth)-printing%5D%3A%20answering%20the%20question%20of%20'WTF%20am%20I%20even%20looking%20at%3F!':%5B%5BBlue2thprinting%20(blue-%5Btooth)-printing%5D%3A%20answering%20the%20question%20of%20'WTF%20am%20I%20even%20looking%20at%3F!'%5D%5D%20%5B%5BBluetooth%20Security%20Timeline%5D%5D%20%24%3A%2FTagManager) by Xeno Kovah  
[2] [SweynTooth: Unleashing Mayhem over Bluetooth Low Energy](https://darkmentor.com/bt.html#SweynTooth%3A%20Unleashing%20Mayhem%20over%20Bluetooth%20Low%20Energy:%5B%5BSweynTooth%3A%20Unleashing%20Mayhem%20over%20Bluetooth%20Low%20Energy%5D%5D%20%5B%5BBrakTooth%3A%20Causing%20Havoc%20on%20Bluetooth%20Link%20Manager%20via%20Directed%20Fuzzing%5D%5D%20%5B%5BBluetooth%20Security%20Timeline%5D%5D%20%24%3A%2FTagManager) by Matheus E. Garbelini et al.

## Vendors with VSC present

* [Espressif](../vendor/Espressif.md)