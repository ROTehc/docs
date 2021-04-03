Implementation
===============

.. admonition:: Assumptions
	:class: warning

	- Security is not considered in the current implementation.


Our system architecture is based on OneM2M Service Layer developed by engineers from European Telecomunications Standards Institute. There is a infrastructure node called CSE, a network of nodeMCU devices with gas sensors distribuited all over the territory, and an Infrastructure Application Entity to visualize the data.

.. image:: resources/arch.jpeg
	:align: center

In the case of scaling the project nationwide, middle nodes could be created with their own CSE for each city. One of the advantages of OneM2M is its scalability.

.. image:: resources/arch2.jpeg
	:align: center

.. warning:: Tha nationalwide architecture is only an idea, it was not implemented due to the limited scope of the Hackaton.


in-CSE: ACME
-------------

The institutioinal CSE is built over `ACME <https://github.com/ankraft/ACME-oneM2M-CSE>`_, an open-source light implementation of subset of oneM2M standard specializations written in Python.

.. image:: resources/acme_sm.png
	:align: center
	:width: 150

AE: nodeMCU
------------

The nodeMCU is a low-cost open-source IoT platform. Its firmware runs on the ESP8266 Wi-Fi SoC.

This device has several gas sensors as MG-811 in order to measure the CO2 in air. It also counts with a LCD display to show some operational information.

.. image:: resources/mk1.jpg
	:align: center

When the it is impossible to suply power to the device, there is a Lite version, equiped with a 18650 battery and a small solar panel. In addition, the device doesn't have LCD display and enters in deep sleep when not in use to save energy.

.. image:: resources/lite.jpg
	:align: center
	
Every nodeMCU sends its data every minute to the CSE over HTTP POST requests.

.. warning:: This devices are only prototypes. Correct operation is not guaranteed.


in-AE
------

The infrastructure application entity consists of a web application written in JS which receives data from the CSE and displays it on a map.

Each nodeMCU has some coordinates associated with it. These points are distributed over the territory, forming cells according to Voronoi diagrams, to assign an region of ​​operation to each nodeMCU in an equitable way.

.. image:: resources/voronoi.png
	:align: center
	:width: 350

The app pulls every nodeMCU sensor data from the CSE, and plots it almost in real time.
