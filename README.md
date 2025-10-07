# Chess Board Power Usage considerations
some power considerations for building a chess board like our Youtube videos  
https://www.youtube.com/@builtclever
<hr>
I used AI to help figure this out, so please double-check everything for yourself, information is provided at your own risk.

to check the current needed for choosing a power supply

🔧 Highly Recommended Tips:
* Use a capacitor across the power rails (not inline) to buffer sudden current spikes when LEDs switch on.

* For longer LED runs—even just 64 LEDs—inject power at both the start and end of the strip.

* (VERY IMPORTANT) Add a physical switch to disconnect the LED power (+5V line). Always switch it off before connecting your Arduino to a computer for programming or debugging. Otherwise, the LEDs may try to draw too much current from the USB port.  
 <br />🔌 USB Port Current Limits:
  - USB 2.0: 0.5 A
  - USB 3.0: 0.9 A
  - USB-C: 3.0 A
<br/>
We used the WS2812B 5050 RGB LED Strip (30 LEDs/m, 5V, individually addressable). Ours is a 5-meter strip → 30 × 5 = 150 LEDs

🔋 LED Power Draw:
* Max draw per LED: 60 mA (full white)
* Typical draw: 20–30 mA (animations, partial brightness)

If you light 64 LEDs at full white: 
→ 64 × 60 mA = 3.84 A 
→ Power = 5V × 3.84 A = 19.2 W

Mixed colors: 
→ 64 × 30 mA ≈ 1.92 A
<hr>
We use a 2A 5V phone charger for our board with 1 LED per square.

At most, we show:
* All valid moves for a piece
* The last move made
* Or an error state (all outer squares lit red)
* Plus a 12-LED ring for player turn and thinking animation

Also include
* Hall effects take about 4mA, we only power 8 at a time using the matrix, 8 x 4ma = 32mA
* arduin Nano = (30 - 60ma) approx

🧠 Example: Queen with Many Moves  
 Vertical & Horizontal: 7 squares each → 14 LEDs  
 Diagonals: 7 squares each → 14 LEDs  
 Total valid moves: 28 LEDs  
 Last move (start + end): 2 LEDs  
 LED ring: 12 LEDs → Max active LEDs: 28 + 2 + 12 = 42 LEDs  
 We don’t run full brightness on the ring, especially for white.  

🔋 Power Breakdown:  
LED ring: 12 × 45 mA = 540 mA  
Board LEDs: 28 × 40 mA = 1120 mA  
Hall sensors: 8 × 4 mA = 32 mA  
Arduino Nano: 30–60 mA 
Total: 1,752ma  1.7 A
Leaves a bit of headroom for color variations or brief spikes.  

🧮 If You were to use for example 4 LEDs per Square:  
Using my rules above 540 mA × 4 = 2.16 A   
At full white brightness: → 64 × 4 × 60 mA = 15.36 A, just for the LEDs!    

When we also use the motors to try and move the pieces with magnets  
NEMA 17 can be approx (1.2A to 2A peak) x 3 = max 6A  
so we used a computer power supply rated for 20A to be over confident  
also has the benifit of have 12v and 5v power lines  

please double check all this yourself, 
AI is a great help with it but best to be sure
