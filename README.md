# Vending Machine Circuit 

<img src="https://raw.githubusercontent.com/bedrockskeleton/vending-machine/refs/heads/main/images/vending.jpg" alt="Nice picture of my vending machine circuit with the power supply" height="300">

The purpose of this repository is to demonstrate a mock vending machine ciruit built on a breadboard with just some switches, wires, LEDs, resistors, and two integrated circuits. Later, I'll demonstrate how this wiring can be simplified with a Raspberry Pi. The heart of this circuit is the SR latch, which can be made with a single 7402 IC. The SR latch functions much like a transistor, able to hold a single bit of memory.

<img src="https://raw.githubusercontent.com/bedrockskeleton/vending-machine/refs/heads/main/images/sr-latch.png" alt="SR latch circuit diagram" height="300">

Unlike a transistor though, an SR latch has two simple inputs: one to set and store the bit, and another to erase and reset the latch. In the above image, these set and reset inputs are marked with an S and R, respectively. The output is marked with a Q and leads to a resistor and LED that glows when the the latch is set. This type of circuit is useful for many things; mainly when you need one input to activate something, and another to then turn it off. A famous example is in vending machines; where inserting money "activates" the vending machine and selecting an item/returning the money "turns it off".

<img src="https://raw.githubusercontent.com/bedrockskeleton/vending-machine/refs/heads/main/images/vending-circuit-diagram.png" alt="Circuit diagram for a mock vending machine" height="300">

This is a diagram of the circuit I'll be building. It features the SR latch along with some extra components to make it more realistic. Namely there is a 7408 (AND) IC and a capicator. The capacitor gives the VEND button a little delay before resetting the SR latch, and the AND gate makes sure the capacitor only fills up when the latch is set. This also causes the VEND LED to only shine for a brief moment before turning itself and the COIN LED off. Below you can see the completed circuit with some labels.

<img src="https://raw.githubusercontent.com/bedrockskeleton/vending-machine/refs/heads/main/images/labeled-vending-close.png" width="100%">

When you press the COIN button, the latch is set and the COIN LED illuminates. This simulates a user putting the required amount of money into the vending machine, signaling to it that it's ready to vend.

<img src="https://raw.githubusercontent.com/bedrockskeleton/vending-machine/refs/heads/main/images/labeled-vending-coin.png" height="300">

With the COIN LED lit up, you can then press and hold the VEND button to simulate recieving your item. Holding the button is necessary to charge the capacitor and trigger the SR latch to reset. The first image below shows what happens as soon as you press the VEND button, and the second shows the lights after about a second of holding it.

<img src="https://raw.githubusercontent.com/bedrockskeleton/vending-machine/refs/heads/main/images/labeled-vending-vend.png" height="300"><img src="https://raw.githubusercontent.com/bedrockskeleton/vending-machine/refs/heads/main/images/labeled-vending-vend-off.png" height="300">

The advantage of this setup over a standalone SR latch is that the action comes after the condition is set. If I built a working vending machine with just an SR latch, it would drop my snacks as soon as I put the money in. This is not ideal, so the AND gate allows the user to insert money and then take time to decide what they want. Another advantage is modularity. With a single latch, this system could be expanded with multiple VEND buttons controlling different LED's to simulate the different snack choices a real machine would have to offer.

## Offloading Logic to a Raspberry Pi

Using a Raspberry Pi in our circuit greatly simplifies our breadboard wiring. We can omit the IC chips, capacitors, and one of the LEDs in favor of a couple buttons and wires. The most challenging part now is connecting our circuit to the Pi and coding in Python. In order to connect to the Pi's General Purpose Input/Output (GPIO) pins, we need to know what each one does.

<img src="https://raw.githubusercontent.com/bedrockskeleton/vending-machine/refs/heads/main/images/gpio-reference.png" height="300">

This reference image from our book labels each pin and its function. The 3.3 and 5 volt pins constantly supply their respective voltages, and "GND" denotes each ground pin. All the other pins are labeled with GPIO 1 through 26; they'll be the backbone of this project. GPIO pins are responsible for detecting and outputting digital signals. "Digital" means that the pins can only read boolean values (ON or OFF). Voltages below 3.3 volts are considered OFF, while voltages above that are considered ON. For our project, we'll use pins 3, 5, 7, and 9.

<img src="https://raw.githubusercontent.com/bedrockskeleton/vending-machine/refs/heads/main/images/vending-pi-circuit-diagram.png" height="300">

This is the updated wiring diagram for our Pi-based vending machine. 

### Works Cited

Justice, M. (2020). How Computers Really Work: A Hands-On Guide to the Inner Workings of the Machine. No Starch Press.
