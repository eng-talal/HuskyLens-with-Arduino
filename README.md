# Using Arduino to Switch ON an LED When HuskyLens Detects a Face

This guide explains how to use an Arduino to turn on an LED when the HuskyLens detects a face.

## Materials Needed
- Arduino board (e.g., Arduino Uno)
- HuskyLens AI Camera
- LED
- Resistor (220Ω)
- Breadboard and jumper wires
- USB cable for programming the Arduino

## Circuit Setup

1. **Connect the LED to the Breadboard:**
   - Place the LED on the breadboard.
   - Connect the longer leg (anode) of the LED to a digital pin (e.g., pin 7) on the Arduino using a jumper wire.
   - Connect the shorter leg (cathode) of the LED to one end of the resistor.
   - Connect the other end of the resistor to the GND (ground) on the Arduino.

2. **Connect the HuskyLens to the Arduino:**
   - Connect the `TX` of the HuskyLens to the `RX` (pin 10) of the Arduino.
   - Connect the `RX` of the HuskyLens to the `TX` (pin 11) of the Arduino.
   - Connect the `GND` of the HuskyLens to the `GND` of the Arduino.
   - Connect the `VCC` of the HuskyLens to the `5V` on the Arduino.


![HuskyLens Presentation](https://github.com/user-attachments/assets/e72815b2-0e05-4361-ab69-90127a80cb51)



## Programming the Arduino

1. **Install the HuskyLens Library:**

   - install the [HUSKYLENS Library](https://codeload.github.com/HuskyLens/HUSKYLENSArduino/zip/master) and Unzip the file.
   - Open the Arduino IDE.
   - Go to `Sketch` > `Include Library` > `Add.ZIP Libraries`.
   - Select the "HuskyLens" ZIP file you downloaded.

* for more information visit [DFRobot](https://wiki.dfrobot.com/HUSKYLENS_V1.0_SKU_SEN0305_SEN0336#target_28)

3. **Write the Code:**

   ```cpp
   #include <HUSKYLENS.h>
   #include <SoftwareSerial.h>

   HUSKYLENS huskylens;
   SoftwareSerial mySerial(10, 11); // RX, TX
   int LED = 7; // LED connected to digital pin 7

   void setup() {
       pinMode(LED, OUTPUT);
       Serial.begin(9600);
       huskylens.begin(Serial);
   }

   void loop() {
       if (huskylens.request()) {
           if (huskylens.isLearned()) {
               int ID = huskylens.readID(); // Read the ID of the detected object
               if (ID == 1) { // Assuming the face is trained with ID = 1
                   digitalWrite(LED, HIGH); // Turn ON the LED
               } else {
                   digitalWrite(LED, LOW); // Turn OFF the LED
               }
           }
       }
   }

 4. **Upload the Code:**
    
- Connect the Arduino to your computer using a USB cable.
- Select the correct board and port from the Tools menu.
- Click the Upload button to upload the code to the Arduino.


## Testing the Setup

1. **Train the HuskyLens to Recognize a Face:**
   
- Set the HuskyLens to "Face Recognition" mode.
- Point the camera at the face you want to recognize.
- Press the "Learning" button to store the face with ID = 1.

 
2. **Observe the LED:** 

- When the trained face is detected by the HuskyLens, the LED should turn ON.
- If the face is not detected, the LED will remain OFF.

Now you have successfully set up the Arduino to switch on an LED when the HuskyLens detects a face!

<img src="https://github.com/user-attachments/assets/18fb3335-8d40-4b7f-bc1b-a5f2d2cfb42b" alt="Screenshot" width="600">

<img src="https://github.com/user-attachments/assets/f6b498a3-7a08-4deb-8d2d-602e9343041d" alt="Screenshot" width="600">
