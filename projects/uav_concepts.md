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
<h2>Concept</h2>

Below are the original sketches of the general concept. As the saying goes "a picture is worth a thousand words", I find it easier to describe the overall concept by showing various sketches and renders. All modeling and rendering was done in Solidworks. My typical workflow is to draw a rough sketch of the idea, ensure it makes sense on paper and then start modeling it in CAD.

The overall concept is one of two aircraft; a primary designated "Mother" and a secondary designated "Reserve". Mother is designed for maximum endurance carrying a surveillance package, while Reserve is designed for maximum payload capacity to haul two sets of batteries around. Reserve was orignally conceived to be a fixed-wing, tilt-rotor configuration with VTOL (Vertical Takeoff and Landing) capability. The original idea was to maximize payload capacity as well as range. However, after realizing the complexity of the control system needed to perform the docking manuever, Reserve was changed to a quadcopter configuration. This allows for VTOL capability, as well as much simpler flight controls for the docking sequence.

<h4>Initial Concept Sketches</h4>
<img class="img-fluid" src="../img/uav_project/concepts/overview.png">
<img class="img-fluid" src="../img/uav_project/concepts/drawing.png">

<h4>Version 1.0 Sketches</h4>
The first version of the docking system was of a mechanical apparatus consisting of two plates mounted on a member protuding from the top of Reserve, meshing into a groove set into the underside of Mother with two opposing plates catching the Reserve plates to lock the aircraft into place. Also visible in the sketches are early ideas for the battery attachment.

The first concept of the docking arm. The idea is to use the weight of Reserve to hold the aircraft together. This is accomplished through the use of pulleys at opposite ends of the system. Overall sizing is dictated by the volume required for the batteries.

<img class="img-fluid" src="../img/uav_project/concepts/docking_arm1.png">
<img class="img-fluid" src="../img/uav_project/concepts/docking_arm2.png">

An earlier version using gears to actuate the plates. The gears were quickly replaced with cables due to the efficiency of holding the plates in tension, rather then relying on the torque in the gears.

<img class="img-fluid" src="../img/uav_project/concepts/docking_battery_mech_iso_v2.png">

A front view of the docking system. Note the two cables on the lever providing opposing force to either grab or release the center member. The weight of Reserve produces a downward moment on the levers. This is opposed by the second cable mounted at the end of the lever and routed around the pulleys at the ends. 

<img class="img-fluid" src="../img/uav_project/concepts/docking_battery_mech_front.png">
<img class="img-fluid" src="../img/uav_project/concepts/docking_battery_mech_top.png">

The cables are mounted to a cross member that can translate along the longitudinal axis of the system. As the cross member slides towards the levers, the dock is engaged. Likewise, then the cross member slides away from the levers the dock is released.

<img class="img-fluid" src="../img/uav_project/concepts/docking_mech.png">
<img class="img-fluid" src="../img/uav_project/concepts/docking_battery_mech_iso_v1.png">

<h3>Analysis</h3>

After the initial design was finalized, an analysis was performed on the arm and cable system to ensure it produced enough force to hold the two aircraft together.

<img class="img-fluid" src="../img/uav_project/concepts/FBD.png">
<img class="img-fluid" src="../img/uav_project/concepts/arm_moment.png">
<img class="img-fluid" src="../img/uav_project/concepts/dynamics.png">

<a href="Docking-Battery Mechanism M-1.pdf">Docking-Battery Mechanism Moment of Inertias</a>

<a href="Docking-Battery Mechanism M-1 Analysis.pdf">Docking-Battery Mechanism Analysis</a>

The required force to connect the two aircraft was found though analyzing the rigid-body dynamics of the arm-pulley assembly. To connect the two aircraft together, a max torque of 13oz-in is required in the arms and approximately 2.4 lbs-force in the cables. Assuming a factor of safety of 1.5 and rounding up, equates to a max tension of 4 lbs-force or about 18 newtons. The <a href="https://www.actuonix.com/assets/images/datasheets/ActuonixL12Datasheet.pdf">Actuonix L12-R Micro Linear Servo</a> was chosen with a gearing of 100:1 which provides 42 newtons of force to ensure an adequate margin accounting for wind gusts.

<h3>Docking System</h3>

<h5>Position 1</h5>

Levers in released position. Center groove is empty. Aircraft are undocked. Noticed how the first cable was replaced by a spring to keep tension in the cables when the levers are released.
<img class="img-fluid" src="../img/uav_project/concepts/M-1_R-1 Docking System Closeup Undocked.png">

<h5>Position 2</h5>

Levers in released position, center member is inside groove. Aircraft are midway through docking sequence.
<img class="img-fluid" src="../img/uav_project/concepts/M-1_R-1 Docking Systems Closeup Undocked.png">

<h5>Position 3</h5>

Levers in engaged positon, center member is pressed against groove. Aircraft are docked.
<img class="img-fluid" src="../img/uav_project/concepts/M-1_R-1 Docking Systems Closeup Docked.png">

<h3>Battery System</h3>

<a href="Docking-Battery Mechanism M-1 Analysis.pdf">Docking-Battery Mechanism Analysis</a>

I originally designed the battery system using a screw approach. A threaded rod would thread into a threaded insert set into the battery holder assembly. This approach ensured a solid connection with minimal force on the motor that drove the assembly. The required torque for the motor was calculated to be 12.3 oz-in with a factor of safety of 1.5. A <a href="https://www.linengineering.com/products/stepper-motors/hybrid-stepper-motors/3709-series/3709V-18">Lin Engineering 3709 Series Hybrid Stepper Motor</a> was selected with a holding torque of 15.58 oz-in to ensure sufficient torque to drive the assembly.

<h4>Version 1.0</h4>
<img class="img-fluid" src="../img/uav_project/concepts/battery_mount_system_v1_iso.png">
<img class="img-fluid" src="../img/uav_project/concepts/battery_mount_system_v1_cross-section1.png">
<img class="img-fluid" src="../img/uav_project/concepts/battery_mount_system_v1_cross-section2.png">

<h3>Complete Assembly</h3>

Final renders showing completed assemblies. Note how large version 1.0 is compared to version 2.0 and 3.0.

<h4>Version 1.0</h4>
<img class="img-fluid" src="../img/uav_project/concepts/M-1 Docking System Iso.png">

<img class="img-fluid" src="../img/uav_project/concepts/M-1 Docking System Back.png">

<img class="img-fluid" src="../img/uav_project/concepts/M-1 Docking System Front.png">

<img class="img-fluid" src="../img/uav_project/concepts/M-1 Docking System Top.png">

<img class="img-fluid" src="../img/uav_project/concepts/M-1 Docking System Extend Bottom.png">

<img class="img-fluid" src="../img/uav_project/concepts/M-1 Docking System Explode.png">

While this approach could work, it has a number of flaws. First it is a fairly complicated approach to merely attach a battery. Second, due to the vertical orientation of the major components, the volume of the fuselage to contain such a system is excessive. The battery has a height of only 2 inches, whereas the total height of the above assembly is over 7 inches. Therefore, I started looking for an approach that resulted in a more compact assembly.

<h4>Version 2.0</h4>

Version 2.0 was designed with a focus on remaining compact while still attaching the battery in an effective manner. However, a few issues were also discovered. First, version 2.0 relies on a sliding assembly, therefore friction is an issue. Second, the assembly is still a little large, 2.5 inches for the assembly.

<img class="img-fluid" src="../img/uav_project/concepts/battery_mount_system_v2_iso.png">

<img class="img-fluid" src="../img/uav_project/concepts/version_2_iso.png">

<h4>Version 3.0</h4>

After I finished designing version 2.0, a thought occured to me, "what would the battery system look like on a final production aircraft?" The biggest problem with both of the above approaches is that they are both mechanical solutions with a large number of components. Reliability becomes an issue on highly complex assemblies due to the increased points of failure. On an aircraft that is intended to fly continually for days or weeks at a time, designing a reliable system is imperative. Both version 1.0 and 2.0 are designed to solve a simple problem; attach and detach a battery rapidly, with minimal power loss, while supplying power to the aircraft. Therefore, I began looking at ways to eliminate all mechanical features in the design.

I first started looking at using electromagnets to attach the batteries, however the large power requirements required to maintain the connection defeats the purpose of designing a system for maximum endurance. This is when I discovered <a href="Electropermanent_Magnets_Knaian.pdf">Electropermanent Magnets</a> and realized that they were perfect for my purpose.