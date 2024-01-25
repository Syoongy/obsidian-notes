# Sensors and Actuators
## Sensors
Measures a physical stimulus/modality (Light, temperature, humidity, etc) and outputs a electronic output (Voltage, current)
_Physical -> Electrical Quantity_

The 3 typical modalities are motion, sound and light
### Motion
Changes in axis, acceleration, etc are measured.
- Utilises Inertial Measurement Units (IMU)
- Comprises Accelerometer (3-axis) + Gyroscope (3-axis) + Magnetometer (3-axis)
#### Accelerometer
Measures linear acceleration and indicates the motion direction.
#### Gyroscope
Measures the angular velocity and indicates rotation.
#### Magnetometer
Measures the magnetic field and indicates the heading using 3 axis
![[Pasted image 20240117160430.png]]
### Sound
- Microphones
	- MEMS Mic, Contact Mic
Measures the frequency of the sound for processing.
#### Passive Applications
Hearing aids, speech recognition and disease diagnostics
#### Active Applications
![[Pasted image 20240117163054.png]]
### Light
Utilises photodiodes/ light sensors along with the photoelectric effect. This measures the output vs light intensity.
#### Applications
![[Pasted image 20240117163212.png]]
![[Pasted image 20240117163234.png]]
### Radio Frequency
- It is an electromagnetic wave used for wireless communication.
- It can be used in multipath propagation (Measure any inteference of the radio frequency between 2 points)
- This allows for gestures, heart rate, sleep, etc... to be sensed
- Privacy reasons (Unable to identify the person or item, just the motion)
### Binary vs Multi-level Sensors
- Binary produces a 0 or 1 state
- Multi-level produces more than 2 values
## Actuators
Converts electrical quantity to another form of energy
(Speaker, LED, vibration motor)
## Selection of sensors
### Considerations
#### Required sensing modalities
1) What contextual information is required
2) What sensor modalitites can be used to obtain said contextual information
3) What things should the IoT devices be deployed on
#### Most suitable sensor for each modality
1) Sensor specification sufficient for application needs
2) Are readings periodic or event-driven
3) Can it provide valid measurements in the operating environment
