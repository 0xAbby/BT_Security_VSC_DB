# Write ROM Patches

## Security-relevance

Many BT chips have a majority of the code for their low level protocols (i.e. LMP/LLCP) implemented in a "mask ROM" composed of assembly code etched into the silicon. However, if this code exists in ROM rather than non-volatile memory, such architectures still require a mechanism to patch functionality & security bugs. Such architectures therefore often implement ROM "patching" mechanisms. These mechanisms allow for the redirection of control flow within ROM code to lead out to corrected code for patches. (The ROM itself remains immutable and unchanged.) Such architectures often redirect control flow either via special hardware registers, or periodic checks baked into the code which call a global function pointer if a default NULL value has been replaced with a non-NULL value.

If there is no digital signature checking on the code which is loaded into a system via ROM patching mechanisms, this can allow an attacker to execute arbitrary code in the context of the ROM's BT stack.


[1] [InternalBlue a Bluetooth Experimentation Framework Based on Mobile Device Reverse Engineering](https://darkmentor.com/bt.html#InternalBlue%20a%20Bluetooth%20Experimentation%20Framework%20Based%20on%20Mobile%20Device%20Reverse%20Engineering) by Dennis Mantz  
[2] [Finding New Bluetooth Low Energy Exploits via Reverse Engineering Multiple Vendors' Firmwares](https://darkmentor.com/bt.html#Finding%20New%20Bluetooth%20Low%20Energy%20Exploits%20via%20Reverse%20Engineering%20Multiple%20Vendors'%20Firmwares:%5B%5BFinding%20New%20Bluetooth%20Low%20Energy%20Exploits%20via%20Reverse%20Engineering%20Multiple%20Vendors'%20Firmwares%5D%5D%20%5B%5BBluetooth%20Security%20Timeline%5D%5D%20%24%3A%2FTagManager) by Veronica Kovah  
[3] [Attacking Bluetooth the easy way](https://darkmentor.com/bt.html#Attacking%20Bluetooth%20the%20easy%20way) by Antonio Vázquez Blanco & Miguel Tarascó Acuña  
[4] [Reverse engineering Realtek RTL8761B* Bluetooth chips, to make better Bluetooth security tools & classes]() by Xeno Kovah & Veronica Kovah  
[5] [Spectra: Breaking Separation Between Wireless Chips](https://darkmentor.com/bt.html#Spectra%3A%20Breaking%20Separation%20Between%20Wireless%20Chips) by Jiska Classen et al.  
[6] [Unlocking the Drive: Exploiting Tesla Model 3](https://darkmentor.com/bt.html#Unlocking%20the%20Drive%3A%20Exploiting%20Tesla%20Model%203) by David BERARD & Vincent DEHORS

## Vendors with VSC present

* [Broadcom](../vendor/Broadcom.md)
* [Cypress](../vendor/Cypress.md)
* [Realtek](../vendor/Realtek.md)
* [Texas Instruments](../vendor/TexasInstruments.md)
