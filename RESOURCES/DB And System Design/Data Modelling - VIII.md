
# Introduction
- Breakout room activity for design
	- Find the schema and tables
		- Mobile Devices , (android, ios or anything else) with various properties
		- OS, Color, Aspect Ratio, Mfg, ... along with owner details.
		- We need to send data (battery% and GPS to server).
		- History of data.

# Breakout Room Activity (Phone - GPS, Battery)
- User Table :
	- User_id | User_name | ...
- Device Table :
	- Device_id | Device_name | .....
- Model Table :
	- Company | Model_Id | Processor ...
- Model Details :
	- Model_id | Variant } color | RAM .....
- Health Data
	- health_id | device_id | battery | long | lat | timestamp | ....


