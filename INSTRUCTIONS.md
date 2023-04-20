# Build Instructions and Notes

### Operating Principles

This project involves the [phase-angle control](https://electricalacademia.com/electronics/scr-thyristor-phase-control-circuit/) of AC signals. this allows for accurate power delivery but it is important to remember that rotational speed of the blender $\neq$ power.

<img src="./Images/Blender_Motor_Wiring_schem.png"  width="600">

_Very basic wiring of a dimmer module with potentiometer control or arduino control, depending on the circuit._

This particular build is a step between potentiometer and arduino control, as the dimmer module comes in two parts; a screen with tactile switches effectively acting as an arduino, and a dimmer module with an arduino interface. The markings on the back of the screen state SCR (GATE), ZERO (Z-C), GND and 5V (VCC). So effectively one could replace the screen with an arduino to achieve Phase Angle Control directly.

Note also, that I found it possible to measure the speed simply from the noise given off by the blender with the [spectroid app for android](https://play.google.com/store/apps/details?id=org.intoorbit.spectrum). Will take some work to recognise which signals are which, but if you are uninterested in exact speed, you can make the setup more repeatable by aiming for previously obtained resonant frequencies!

##### Phase Angle Control

Phase angle control, is a method of controlling the duty cycle of an AC signal every half cycle. This typically uses a triode called a triac sometimes also called a Silicon Controlled Rectifier (SCR) or a Thyristor, and you will often see these terms banded around when shopping circuitry. The circuit is similar to what you would find in a dimmer switch in a house, hence sometimes it is called a dimmer or dimming circuit.

The main advantages to this type of rectification compared to other similar functioning circuits is that:

1. It does not disapate very much energy.
2. Simple to implement.
3. Duty cycle is small for mains AC (100% $\sim 10\;ms$), so the power delivery is pretty constant (no flickering).

<img src="https://www.libratherm.com/wp-content/uploads/2020/06/2.1-phase-angle-control-representation.jpg">

_Simple representation of phase angle control._

The AC signal in potentiometer controlled cases is routed through a voltage divider which feeds into the GATE pin of the Triac. The exact electronics and some of the issues surrounding these circuits is well discussed in [this article](https://eepower.com/technical-articles/alternating-current-ac-load-control-with-triacs/#). In arduino controlled units, there will be some sort of isolation between the low and high voltage side, primarily through the use of an optocoupler or [similar circuitry](https://www.circuitar.com/nanoshields/modules/triac/).



## Bill of Materials

|Item                   |Link                                                                                 |Qty|Price per Unit|Cost   |Description                                                               |
|-----------------------|-------------------------------------------------------------------------------------|---|--------------|-------|--------------------------------------------------------------------------|
|AMZChef NY-8088MJD     |https://www.amazon.co.uk/Smoothie-AMZCHEF-Commercial-Container-25000RPM/dp/B08CKTB6Z4|1  |£150.00       |£150.00|Top of the line commercial blender, resistant to some solvents.           |
|Walfront Dimmer Circuit|https://www.amazon.co.uk/Digital-Voltage-Regulator-Control-Thermostat/dp/B076VKJM42  |1  |£17.43        |£17.43 |Easy to use, and has the potential for wiring in a separate board.        |
|Heat Shrink            |                                                                                     |-  |-             |-      |To protect soldered collections.                                          |
|Soldering iron         |                                                                                     |-  |-             |-      |Solder wires together.                                                    |
|Red wire 20 awg        |https://www.amazon.co.uk/Electrical-Wire-AWG-Extension-Brightfour/dp/B07CGKCJFV      |-  |-             |-      |Live wiring, of good gauge to handle the current.                         |
|Black wire 20 awg      |https://www.amazon.co.uk/Electrical-Wire-AWG-Extension-Brightfour/dp/B07CGKCJFV      |-  |-             |-      |Neutral wiring, of good gauge to handle the current.                      |
|3DP Bolt-on box        |                                                                                     |-  |-             |-      |To isolate the live AC and be a little safer, also allow a little airflow.|
|3DP Backing Plate      |                                                                                     |-  |-             |-      |To eliminate the need for nuts to fix in the bolt-on box.                 |
|M4 countersink 15 mm   |https://uk.rs-online.com/web/p/socket-screws/0171837                                 |5  |£0.20         |£1.00  |To bolt the lid shut!                                                     |
|                       |                                                                                     |   |              |£168.43|                                                                          |


## Mods

There are no direct modifications to the blender itself, apart from wiring in the dimmer module. In my case, I decided to remove the connections to the main switch dial at the front of the blender, as it didn't add any extra security or control to the blender.

Note that there are much cheaper [pot dimmer circuits](https://www.amazon.co.uk/AITRIP-Control-Controller-Adjustable-Regulator/dp/B08L7NF4Q9) available (at £4.50 a pop), but we decided to go with the overkill option to save any potential headaches. With pot blenders, you can't exactly return to the same power setting unless you have some readout to go with it, for example, a frequency, a precise angle or a power reading. There are [modules](https://www.amazon.co.uk/gp/product/B076VKJM42) which have digital readouts for a more precise reading. Again it is important to stress that precise power $\neq$ precise speed reading.

### Wiring

![Opened blender with labelled modifications](./Images/Hacking_Guide.png)

1.	Unsolder the black wire from the motor to the control switch. This lead is the LIVE AC OUT (**L AC-MOTOR**) to the motor.
2. Unsolder the Yellow Wire from the control switch. This is the LIVE AC IN (**L AC-IN**) to the dimmer.
    
    At this point, the control switch is completely bypassed, but the safety switch isn't. I prefer to keep the safety switch wired in, as it ensures the blender is not live when the jug isnt plugged in.
    
    During my testing, position "P" and "2" on the dial were a simple on off switch (for full AC Power), while position "1" cut the negative half of the waveform.
    
3. The white wire is neutral mains, wired directly to the motor. Cut the wire roughly halfway. This is NEUTRAL AC OUT (**N AC-MOTOR**) to the motor.
4. The other side of the wire cut cut in step 3 is NEUTRAL AC IN (**N AC-IN**) to the Dimmer.

You'll need about half a meter of suitable guage wiring to extend these wires out of the blender. These will take a bit of current, so ensure they are soldered well.

### Printing

CAD files for printing the box are given in the `CAD` folder. There's not much to go into here, as the box offers no extra safety except to hide the wired connection points.

![Blender servo arm](./Images/Dimmer-v1.png)

_Potentiometer blender with added servo._
