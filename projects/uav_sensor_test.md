---
layout: sub_project
type: sub_project
image:
title: ""
date: 2023
published: true
labels:
summary: ""
---

<h2>Sensor Test</h2>
<img class="img-fluid" src="../img/uav_project/sensor_test/sensor_test_rig.png">

<h3>Goal:</h3>

<i>Develop method of measuring distance between two aircraft with $$\pm$$ 1cm accuracy<i>

To align both aircraft in space autonomously requires a high level of accuracy and reliability. There are 3 main regions if you will, that R-1 will have to navigate in to successfully dock with M-1. The first, long distance, covers the region of 10 miles to 30 feet(26,400ft-30ft). The second, medium distance, covers the region of 30 feet to 1 foot (30ft-1ft). The third, short distance, covers the region of 1 foot to 1 centimeter (1ft-0.033ft). 

The long distance region is measured by <a href="https://holybro.com/collections/dronecan-h-rtk/products/dronecan-h-rtk-f9p-rover?variant=42737172119741">GPS</a>. The medium region is measured by a <a href="https://www.stereolabs.com/zed-x/">3D stereo camera</a> to accurately line both aircraft up. The final region is measured by <a href="https://www.adafruit.com/product/5396">ToF</a> sensors. The reason a ToF sensor was chosen rather than an <a href="https://www.adafruit.com/product/1031">IR sensor</a>, <a href="https://www.adafruit.com/product/1343">ultrasonic rangefinder</a>, or <a href="https://www.adafruit.com/product/4441">LIDAR sensor</a> is due to the high accuracy needed to dock R-1 with M-1. The IR sensor has a range of 20-150cm with $$\pm$$ 10cm accuracy. The ultrasonic rangefinder has a range of 30-500cm with $$\pm$$ 10cm accuracy. The LIDAR sensor has a range of 5-1000cm with $$\pm$$ 1cm accuracy. Finally, the ToF sensor has a range of 0.1-600cm with a $$\pm$$ 1cm accuracy. 

While the LIDAR has the required accuracy, the minimum distance of 5cm is too large to ensure an accurate dock. Also at $60 each, the sensor is at the higher end of the market. The ToF on the other hand has a minimum distance of 0.1cm. Also at $15 each, the cost is much more economical and allows for multiple sensors to be integrated into the system for increased precision.

Of the 3 regions, the short distance is the most important because it is the zone where the final docking is performed. Therefore, a high degree of accuracy and precision is required to ensure a repeatable system. To develop a precise method of control, testing is necessary to determine the optimal placement of sensors and whether the sensors can accurately detect movement.

<h4>Test Concept</h4>
The initial concept consisted with sensors mounted on a pivot on both sides of the M-1 and R-1 models. The idea was to ensure accurate distance measurements within the Y-Z plane of the two test pieces. The next iteration would involve sensors mounted on pivots on the front and rear of the M-1 and R-1 models to get measurements within the X-Z plane. However, this configuration doesn't account for any rotation outside of these planes. 

The next iteration consisted of sensors mounted in a "X" pattern on R-1 to easily account for any changes in rotation, and the distance measurements were obtained by adjusting the angle of the sensors relative to the M-1 model.

<div class="text-center p-2">
	<img width="600px" src="../img/uav_project/sensor_test/sensor_test_v1.png">
	<img width="600px" src="../img/uav_project/sensor_test/sensor_test_v2.png">
</div>

For an initial test, I wanted to see how much the measured distance deviated from the actual distance of the model. A test rig was constructed to hold the M-1 model steady at a fixed height above the R-1 model. The movement of R-1 was limited along the X-Y axis by following increments marked on the grid of a foam board. This allowed the measured ToF distance to be compared with the actual location marked on the board.

<h5>Sketch of Test Rig</h5>
<div class="text-center p-2">
	<img width="600px" src="../img/uav_project/sensor_test/SCAN0031crop.png">
	<img width="600px" src="../img/uav_project/sensor_test/SCAN0032crop.png">
</div>

<br>

<h5>CAD model of Test Rig</h5>
<div class="text-center p-2">
	<img class="img-fluid" src="../img/uav_project/sensor_test/sensor_test_rig2.png">
</div>

<br>

<h5>3D Printed Test Rig</h5>
<div class="text-center p-2">
	<img class="img-fluid" src="../img/uav_project/sensor_test/3d_printed_model.png">
</div>

<br>

<h4>Test Setup</h4>
To collect the data, an <a href="https://www.adafruit.com/product/3857">Adafruit Feather M4 Express</a> with a <a href="https://www.adafruit.com/product/2922">Adalogger FeatherWing - RTC + SD Add-on</a> and <a href="https://www.adafruit.com/product/2693">SD Memory Card</a> were used. The Feather M4 ran the CircuitPython code to initialize the sensors and write the data to the SD card. The Adalogger housed the SD card and real-time clock. The SD card stored the data to be easily transferred to a computer after the test.  

<div class="text-center p-2">
	<img class="img-fluid" src="../img/uav_project/sensor_test/test_setup_callouts.png">
</div>

<div class="text-center p-2">
	<img width="400" src="../img/uav_project/sensor_test/Test Data-1.jpg">
</div>

The Feather M4 can easily receive data through its I2C port, however its only possible to connect a single address at a time to the Feather. To receive data from multiple sensors, a multiplexer is necessary to select the unique addresses for each sensor. The following code block initializes the Front Right(FR) sensor. Sensors, Back Right(BR), Front Left(FL), and Front Right(FR) are initialized in the same way.

```python
	def ToF_Sensor_FR():
		"""Setup Front Right Sensor"""
		i2c = board.I2C()

		# Create the Mux object and set it to the I2C bus
		tca = adafruit_tca9548a.TCA9548A(i2c)

		# Set the ToF sensor to the Mux
		vl53= adafruit_vl53l4cd.VL53L4CD(tca[3])

		vl53.inter_measurement = 0
		vl53.timing_budget = 10

		# Start measuring values
		vl53.start_ranging()

		# Skip over bad data
		while not vl53.data_ready:
			pass

		# Print distance to screen
		vl53.clear_interrupt()
		print("Distance: {} cm".format(vl53.distance))

		# Wait for 1 millisec
		time.sleep(0.001)

		# Return distance value
		return vl53.distance
```
Code block that loops through each sensor. Outputs a plot on the Mu python editor to see movements of R-1 in near real-time and writes the sensor reading to a text file. Also, grabs a timestamp of the sensor reading and writes it to a text file as well.

```python
	busInc = 0
	elapsed_time = 0
	while True:
		t = rtc.datetime
		start = time.time()

		# Initialize Sensor
		print("Bus number: ", busInc)
		if busInc == 0:
			BR = ToF_Sensor_BR()

			# Store data on SD card
			with open("/sd/sensor_test_data.txt", "a") as f:
				f.write("%0.1f\t" % BR)

		elif busInc == 1:
			BL = ToF_Sensor_BL()

			# Store data on SD card
			with open("/sd/sensor_test_data.txt", "a") as f:
				f.write("%0.1f\t" % BL)

		elif busInc == 2:
			FL = ToF_Sensor_FL()

			# Store data on SD card
			with open("/sd/sensor_test_data.txt", "a") as f:
				f.write("%0.1f\t" % FL)

		elif busInc == 2:
			FL = ToF_Sensor_FR()

			# Store data on SD card
			with open("/sd/sensor_test_data.txt", "a") as f:
				f.write("%0.1f\t" % FR)

		# Plot on X-Y scale
		print(
			(
				(FR),
				(FL),
				(BR),
				(BL),
			)
		)

		# ToF_Sensor(busInc)
		print("")

		end = time.time()
		elapsed_time = end - start

		if elapsed_time >= 1:
			print("The time is %d:%02d:%02d" % (t.tm_hour, t.tm_min, t.tm_sec))

			if busInc == 0:
				# Store elapsed time on SD card
				with open("/sd/sensor_test_time.txt", "a") as f:
					f.write("\n%d:%02d:%02d\n" % (t.tm_hour, t.tm_min, t.tm_sec))

			elif busInc == 1:
				# Store elapsed time on SD card
				with open("/sd/sensor_test_time.txt", "a") as f:
					f.write("\n%d:%02d:%02d\n" % (t.tm_hour, t.tm_min, t.tm_sec))

			elif busInc == 2:
				# Store elapsed time on SD card
				with open("/sd/sensor_test_time.txt", "a") as f:
					f.write("\n%d:%02d:%02d\n" % (t.tm_hour, t.tm_min, t.tm_sec))	

			elif busInc == 3:
				# Store elapsed time on SD card
				with open("/sd/sensor_test_time.txt", "a") as f:
					f.write("\n%d:%02d:%02d\n" % (t.tm_hour, t.tm_min, t.tm_sec))

	busInc += 1
	if busInc == 4:
		busInc = 0

		# Start new line
		with open("/sd/sensor_test_data.txt", "a") as f:
			f.write("\n")
```

$$
X = {L \above{1pt} \cos(\theta_N)}
$$
