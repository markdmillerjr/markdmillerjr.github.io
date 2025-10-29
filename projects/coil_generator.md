---
layout: project
type: project
image: img/pac_project/pac_aircraft.png
title: "Coil Generator Macro"
date: 2017-present
published: false
labels:
  - Excel/VBA
  - Solidworks
  - 2D Plotting
  - Trigonometry
summary: "An Excel macro to automatically generate a coil from a set of inputs."
---

<h3>Project Overview</h3>

In designing PCB motors, a method of drawing the 

Traditionally designing coils is done using scripts to calculate the parameters for each spiral. These spirals are benefical in designing PCB motors due to concentrating the magnetic fields into a shape for an electric motor. However, I wanted to devise a method of calculating the parameters using Solidworks due to that being my primary CAD system.


I wrote this macro to quickly design coils in Solidworks. To do this I used a feature in Solidworks called "Variable Pattern". Variable pattern allows the user to independently adjust each parameter for each subsequent pattern. Solidworks allows the user to upload an Excel file to list each parameter. Since the file