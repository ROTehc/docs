Implementation
===============

Our system architecture is based on OneM2M Service Layer developed by engineers from European Telecomunications Standarts Instritute. There is a infrastructure node called CSE, a network of nodeMCU devices with gas sensors distribuited all over the territory, and an Infrastructure Application Entity to visualize the data.

.. image:: resources/arch.png
	:align: center

in-CSE
-------

nodeMCU
--------

The nodeMCU is a low-cost open-source IoT platform. Its firmware runs on the ESP8266 Wi-Fi SoC.

This device has several gas sensors as MG-811 in order to measure the CO2 in air. It also counts with a LCD display to show some operational information.

.. image:: resources/nodemcu.jpg
	:align: center
	
Every nodeMCU sends its data every minute to the CSE over HTTP POST requests.

in-AE
------

The infrastructure application entity consists of a web application written in JS which receives data from the CSE and displays it on a map.

Each nodeMCU has some coordinates associated with it. These points are distributed over the territory, forming cells according to Voronoi diagrams, to assign an region of ​​operation to each nodeMCU in an equitable way.

.. image:: resources/voronoi.png
	:align: center
	:width: 350

The app pulls every nodeMCU sensor data from the CSE, and plots it almost in real time.
