This document describes features of Stone_multirabber_controller -application

Application is designed to be used to start Voice call, uplink/downlink file transfers using HTTP protocol, SMS sending/receiving and/or Web surfing automation
to multiple UEs or single UE which are having Stone_multirabber -application running.

Version number and color at the top right corner of the Stone_multirabber and Stone_multiraber_controller applications shows the version information of the application.	
If applications are having different versions then tests can be stopped but not started with Stone_multirabber_controller.
	
1. CALL TEST
	Functionality: Sends destination phone number to Stone_multirabber for CALL TEST
	Functions: 	- Pick a contact from phone contact list. 
			- add test UE phone number manually to text box (allowed chars: numbers, +, () )
				- "SW decides number from the list of selected Test UEs" -selection can be used if there is multiple Test UEs to be controlled. When this option is selected application
				decides destination number for each Test UE. UE which application selects as destination then parameter MTC will be sent (Mobile terminated Call). Please use even (2,4,6,8,10,12...etc)
				number of tests UEs when this option is selected! 
				NOTE: Test UEs shall have Automatic answer -function enabled, this might require handset installation.
				NOTE2: When CALL TEST is ongoing in multirabber then other tests might not work on background
		
2. HTTP UL DATA TEST
	Functionality: Sends "Local file name in UE root folder" and "Timeout value in seconds" for HTTP UL DATA TEST
	Functions:	- Local file: Enter local file name manually (example: 10M.bin)
				- Timeout between the transfers: Timeout in seconds for how long application waits until file is uploaded to HTTP server again (example: 15)
				
3. HTTP DL DATA TEST
	Functionality: Sends "Destination file" and "Timeout value in seconds" for HTTP DL DATA TEST
	Functions:	- Destination file name 100M.bin
				- Timeout between the transfers: Timeout in seconds for how long application waits until file is downloaded from HTTP server again (example: 15)
					
4. SMS TEST
	Functionality: 	Sends parameters for SMS TEST 
	Functions: 	- Pick a contact for SMS: NOTE, If contact(s) are not visible (contact is not created/sync`d with Google account) then add destination phone
				number manually to text box (allowed chars: numbers, +, () )
				- SMS field: type SMS text to this field. SMS message lenght is limited to 130 characters.
				- "SW decides number from the list of selected Test UEs" -selection can be used if there is multiple Test UEs to be controlled. When this option is selected application
				decides destination number for each Test UE.
				- Timeout between SMSs: Defines timeout between the SMSs
	
5. WEB VIEWER TEST
	Functionality: Sends web page address for HTTP WEB VIEWER TEST
	Functions: 	- HTTP address for a web page (example: http://www.google.com)
				- Timeout for page reload: Timeout for how long application waits until HTTP web page is reloaded
	
STOP ALL TESTS -button
	Functionality: Stops all ongoing tests from multirabber(s)
	Functions:	- if "Send stats to server" is selected then multirabber sends statistics to multirabber server
			- if "clear stats from Multirabber" is selected then multirabber clears all statistics/counters (after results/stats are sent to server).

TRIGGER -function:
	Trigger functionality can be used to start tests on multirabber(s) automatically when multirabber_controller notices trigger-file.
	
	functionality:  Presetup: fill tests to be run and test UE numbers.
			When a valid path is entered in to "trigger file nam and path" text box and START-button is pressed the Multirabber_controller start polling trigger file from given path.
			Once multirabber_controller gets file from path it starts defined tests for multirabber UEs. 
			TEST SEQUENCE-function can be used together with TRIGGER.
			When Test lenght -timeout expires then TRIGGER sends Stop -command multirabber UE(s). After 5min timeout TRIGGER starts polling trigger path again.

TEST SEQUENCE -function:
	Test sequence -function can be used for define 1, 2 or 3 different sequencies 
		example:
			Sequence 1: DL test
			Sequence 2: DL + UL
			Sequence 3: DL + UL + SMS
			Sequence time in minutes
	Test sequence function shows elapsed sequence time (min) and number of run sequencies
	Abort test sequence -button can be used for aborting Test Sequence functionality in Multirabber_controller. NOTE: Abort does not stop tests on Multirabbers, use normal STOP tests -button
	for this purpose, if needed.
	NOTE: limitation with CALL TEST need to be taken in account if its used (pls see Multirabber documentation)


SELECTING TEST UE PHONE NUMBERS
	There is two ways how to start tests for the multiple UEs:
			1. Create to multirabber_controller UE contacts ONE contact and add multiple phone numbers for it (Test UE phone numbers)
			2. Select option "Add Test UEs manually". This selection opens buttons for creating database to phone internal memory for Tes UE phone numbers.
				- Select Test UE Group: Shows available Test UE Groups
				- insert Test UE phone number manually to the text box
				- Click "Add number to Test Group"
				- Click "Show numbers" to see Test UE phone numbers from selected Test UE group
				- Click "Clear Test UE Group" to clear all Test UE phone numbers from selected Test UE group
			NOTE: Currently there is 1 Test UE Group available
				
START TESTS -button. Generates a control message for each Test UE phone number. Control messages are sent 10 second interval to Test UEs.
Progress bar at the bottom of the screen shows the progress of test activation. Expected Test activation time: n * 10 sec ; where n = amount of Test UEs				
