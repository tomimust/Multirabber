This document describes features and functionalities of Stone_multirabber -application

Application is designed to be used for Voice call, uplink/downlink file transfers using HTTP protocol, SMS sending/receiving and/or Web surfing automation for single UE.
Note, when Stone_multirabber_controller is used for controlling the Stone_multirabber:
	- There is no need to insert any values, paths or parameters to multirabber. All needed parameters are received from Stone_multirabber_controller. Just start the Stone_multirabber -application
	and make sure that both applications are having same versions. If applications are having different versions then tests can be stopped but not started with 
	Stone_multirabber_controller.

Version number and color at the top right corner of the applications shows the version information of the application.	
	
AUTHENTICATION
	Multirabber application requires successfull authentication with server before it can be used.

1. CALL TEST
	Functionality: Makes a phone call to a given number. If call drops then Call Counter is increased and new call is made. Destination UE should have automatic answer
	enabled (some models might require that head set is installed)
	Functions: 	- Pick a contact from phone contact list. NOTE: If contact(s) are not visible (contact is not created/sync`d with Google account) then add destination phone
				number manually to text box (allowed chars: numbers, +, () )
				- START CALL TEST -button: starts the call 
	Related counters: 	"# of calls" 
	
2. HTTP UL DATA TEST
	Functionality: Uploads a file/image from given UE folder to HTTP server by using HTTP protocol
	Functions:	- Timeout between the transfers: Timeout in seconds for how long application waits until file is uploaded to HTTP server again (example: 15)
			- Local file: Enter local file name from UE root folder for UL test, example: 1M.bin
			
	Related counters:	Successfull and failed HTTP put file operations "# of UL file"
	
3. HTTP DL DATA TEST
	Functionality: Downloads a file from given HTTP server address by using HTTP protocol
	Functions:	- Destination file name, example 100M.bin
			- Timeout between the transfers: Timeout in seconds for how long application waits until file is downloaded from HTTP server again (example: 15)

	Related counters:	Successfull and failed HTTP get file operations "# of DL file"
					
4. SMS TEST
	Functionality: 	Sends SMS to selected phone number. 
	Functions: 	- SMS field: type SMS text to this field. Message lenght is not limited and any characters are allowed.
			- Pick a contact for SMS: NOTE, If contact(s) are not visible (contact is not created/sync`d with Google account) then add destination phone
			number manually to text box (allowed chars: numbers, +, () )
			- Timeout between SMSs: Defines timeout between the SMSs

	Related counters:	"#of SMSs sent/received"
	
5. WEB VIEWER TEST
	Functionality: Opens the given HTTP web page  
	Functions: 	- HTTP address for a web page (example: http://www.google.com)
			- Timeout for page reload: Timeout for how long application waits until HTTP web page is reloaded
	Related counters: Successfull and failed web page reloads (" of web views")

Multirabber calculates throughput (mbps) when UL and/or DL test is started.
	- Throughput calculates and shows values for Min, max, ave and last data transfer operations in mbps.

Clear all counters -button sets all counter values to zero (0). This can be done without stopping the tests.

STOP ALL TESTS -button. Stops all ongoing tests. Note, if there is large file download/upload ongoing, please wait until it is finished before starting new tests.

KNOWN LIMITATIONS:
		Throughput calculations are done for following files: 1M.bin, 10M.bin, 100M.bin, 1G.bin, 50M.bin, 500M.bin
		All other tests are running on background except CALL TEST. This means that if CALL TEST and some other tests are started at the same time, only call test will be executed.
		Application main screen have to be visible/active when tests are running. 
		Workaround how to execute CALL TEST and other tests at the same time:
			- START CALL TEST
			- Go back to Stone_multirabber -application main screen
			- Start other tests
			Expected behaviour: All tests are running as long as Call is not dropped/hangout. When call is terminated then application automaticly re-establishes the call and call 
			screen stays visible/active. Then other tests are not running until application main screen is active/visible again.