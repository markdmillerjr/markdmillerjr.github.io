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

<h3>Sensor Test</h3>
<img class="img-fluid" src="../img/uav_project/sensor_test/sensor_test_rig.png">

<h4>Goal:</h4>

<i>Develop method of measuring distance between two aircraft with $$\pm$$ 1cm accuracy</i>

To align both aircraft in space autonomously requires a high level of accuracy and reliability. There are 3 main regions if you will, that R-1 will have to navigate in to successfully dock with M-1. The first, long distance, covers the region of 10 miles to 30 feet(26,400ft-30ft). The second, medium distance, covers the region of 30 feet to 1 foot (30ft-1ft). The third, short distance, covers the region of 1 foot to 1 centimeter (1ft-0.033ft). 

The long distance region is measured by <a href="https://holybro.com/collections/dronecan-h-rtk/products/dronecan-h-rtk-f9p-rover?variant=42737172119741">GPS</a>. The medium region is measured by a <a href="https://www.stereolabs.com/zed-x/">3D stereo camera</a> to accurately line both aircraft up. The final region is measured by <a href="https://www.adafruit.com/product/5396">ToF</a> sensors. The reason a ToF sensor was chosen rather than an <a href="https://www.adafruit.com/product/1031">IR sensor</a>, <a href="https://www.adafruit.com/product/1343">ultrasonic rangefinder</a>, or <a href="https://www.adafruit.com/product/4441">LIDAR sensor</a> is due to the high accuracy needed to dock R-1 with M-1. The IR sensor has a range of 20-150cm with $$\pm$$ 10cm accuracy. The ultrasonic rangefinder has a range of 30-500cm with $$\pm$$ 10cm accuracy. The LIDAR sensor has a range of 5-1000cm with $$\pm$$ 1cm accuracy. Finally, the ToF sensor has a range of 0.1-600cm with a $$\pm$$ 1cm accuracy. 

While the LIDAR has the required accuracy, the minimum distance of 5cm is too large to ensure an accurate dock. Also at $60 each, the sensor is at the higher end of the market. The ToF on the other hand has a minimum distance of 0.1cm. Also at $6 each, the cost is much more economical and allows for multiple sensors to be integrated into the system for increased precision.

Of the 3 regions, the short distance is the most important because it is the zone where the final docking is performed. Therefore, a high degree of accuracy and precision is required to ensure a repeatable system. To develop a precise method of control, testing is necessary to determine the optimal placement of sensors and whether the sensors can accurately detect movement.

<h4>Test Rig</h4>
<h5>Sketch</h5>
<div class="text-center p-2">
	<img width="600px" src="../img/uav_project/sensor_test/SCAN0031.png">
	<img width="600px" src="../img/uav_project/sensor_test/SCAN0032.png">
</div>

<p>

<h5>CAD Model</h5>
<div class="text-center p-2">
	<img class="img-fluid" src="../img/uav_project/sensor_test/sensor_test_rig2.png">
</div>

<p>

<h5>3D Printed Model</h5>
<div class="text-center p-2">
	<img class="img-fluid" src="../img/uav_project/sensor_test/3d_printed_model.png">
</div>

<p>

<h5>Test Setup</h5>
<div class="text-center p-2">
	<img class="img-fluid" src="../img/uav_project/sensor_test/test_setup.png">
</div>


<a href="Docking System Equations.html">Equations</a>


Math block:

$$
\displaystyle
\left( \sum_{k=1}^n a_k b_k \right)^2
\leq
\left( \sum_{k=1}^n a_k^2 \right)
\left( \sum_{k=1}^n b_k^2 \right)
$$