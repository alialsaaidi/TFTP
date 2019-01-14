Please see report as this readme is an informal issue.

Sysc 3303 Iteration 5
=====================

==============================================================================================================
What's new? 
--------------------------------------------------------------------------------------------------------------
The client's user interface was modified to allow the user to specify the identity of the host where the server 
will run, and the code that looks up the Internet address of the server's host was modified.
==============================================================================================================
Design decisions 
--------------------------------------------------------------------------------------------------------------
1. To select modes (Octet and ASCII), if a file has a file extention ".txt" or ".cc" or ".java" or ".h" then 
   the program considers it to be a text file. If it is any other file extention, then it is considered a data file.
2. We chose to resend last packets during yhr final transmission of a file until the host retries 4 times,
   then the transfer is considered done.
3. When the client tries to write a file on the server and a file with the same name already exists in the server, 
   users cannot overwrite files on the server (write request). On the client side, the files with same names are 
   overriden (read request).
4. On the error simulator, we  have decided to have an option to either mess with the packets going to the client or 
   with the packets going to the server
5. While performing a write request, it is required to enter the file path. While performing a read request,  
   the user is only required to enter the file name to be read
6. If client tries to write a file, but the file they are trying to write is in a folder which they DO NOT have 
   permission to, we choose to return "File does not exist" error our system believes that since the file cannot 
   be accessed, then it must not exist.
7. We asked the user to enter 1050ms or more because we think that any delay less than 1.05s is not very noticable. 
   This design decision was made so that the user can notice the packet being delayed.
8. Why is the error simulator run on the same computer as the client and not with the server? This is because our design allows 
   us to simulate unique errors for each client ans server interaction and the file transfers are innitiated by the client. 
==============================================================================================================
Some things that'll eventually be fixed (from the previous iterations)
--------------------------------------------------------------------------------------------------------------
1. Moving configurations to a text file so that the program doesn't need to be recompiled in order for the changes to 
   take in effect (for error code 3: Disk full or allocation exceeded)
**************************************************************************************************************
==============================================================================================================
General Set up Instructions 
--------------------------------------------------------------------------------------------------------------
1. Start up two computers: Computer A and Computer B
2. Do the following in both computers: 
	2.1. Extract this folder into a location on your computer
	2.2. Open Eclipse (Mars.1) and select the workspace path
             of where you extracted the assignment
3. Do the following in computer A:
	3.1. Open two consoles. One for the UI of TFTPClient.java and the other for the UI of ErrorSimulatorServer.java.
	3.2. Run ErrorSimulatorServer.java and set up your preferences according to the general UI option selections 
	     for ErrorSimulatorServer.java described below. (please scroll down)
	3.3. Run TFTPClient.java and set up your preferences according to the general UI option selections 
	     for TFTPClient.java described below. (please scroll down)
4. Do the following in computer B:
	4.1. Open one console for the UI of TFTPServer.java
	4.2. Run TFTPServer.java and set up your preferences according to the general UI option selections 
	     for TFTPServer.java described below. (please scroll down)
5. Folders "/TFTP-Server-Storage-Folder" and "/TFTP-Client-Storage-Folder" will be created automatically under your home. 
   This is the location where the resulting files will be saved under. 
	5.1. If you want to change the location of the these folders, please change the absolute path string of the variable USER_HOME
             in Configurations.java
	5.2. [Server folder] has files uploaded from the client to the server.
	5.3. [Client folder] has files downloaded from the server to the client
	5.4. If you're on windows it is:
		5.4.1. C:\Users\<user name>\TFTP-Server-Storage-Folder
        	5.4.2. C:\Users\<user name>\TFTP-Client-Storage-Folder
   	5.5. If you're on linux it is
        	5.5.1. /Users/username/TFTP-Server-Storage-Folder
        	5.5.2. /Users/username/TFTP-Client-Storage-Folder
==============================================================================================================
General UI option selections for TFTPServer.java 
--------------------------------------------------------------------------------------------------------------
1. When prompted: Logging should be (1) silent or (2) verbose? Please select whether detailed information about 
   the program's execution should be given (Verbose) or omitted (Silent)
2. If you wish to shut-down the server, the server shutdown sequence can be initiated at any time 
   by pressing 'q' on the command line.
==============================================================================================================
General UI selections for ErrorSimulatorServer.java
--------------------------------------------------------------------------------------------------------------
1. When prompted: 
   	Hosting at:
	 	1. Local host
	 	2. Remote host
   Please select 2 (Remote host) to simulate errors between two computers with the client and the server on one computer and the server
   on the other.
2. When prompted: 
	Enter valid host ip: 
   Please enter the ip address of Computer B which is running TFTPServer.java

3. When prompted: 
	----------------------
	| Error Selection Menu |
	----------------------
	Please select which error to generate
	Options : 
	 	1.Illegal TFTP operation 
	 	2.Unknown transfer ID 
	 	3.No errors please 
	 	4.Transmission Error 
	 	5.Exit 
	Select option : 
   3.1. Please select option 3 to simulate no errors while running the client on the test mode
   3.2. Please select option 5 to sut-down the error simulator
   3.3. When option 1 : Illegal TFTP operation is selected, the following menu is prompted:
	----------------------
	| Illegal TFTP Operation Menu |
	----------------------
	Please select the packet type to simulate on:
	Options : 
	 	0.Go back to the Error Selection Menu 
	 	1.First packet
	 	2.ACK packet
	 	3.DATA packet
		4.ERROR packet
	Select option : 
	3.3.1. Please select option 0 to go back to the error selection menu
	3.3.2. Please select either option 1; 2; 3 or 4 to create an illegal TFTP operation error on either the first packet (RRQ/WRQ);
	       ACK packet; DATA packet or an ERROR packet repectiveley. 
	3.3.3. When option 1: first packet is selected, the following menu is prompted:
		----------------------
		| Corrupt first packet Menu |
		----------------------
		Please select which error to generate
		Options : 
			 0.Go back to the Error Selection Menu 
			 1.Invalid file name (WRQ/RRQ) 
			 2.Invalid packet header during transfer 
	 		 3.Invalid zero padding bytes (WRQ/RRQ) 
	 		 4.Invalid mode (WRQ/RRQ) 
		Select option : 

	       3.3.3.1. Please select how you would like to corrupt the first packet
	3.3.4. When option 2: ACK packet is selected, the following menu is prompted:
		----------------------
		| Ack packet Menu |
		----------------------
		Please select which error to generate
		Options : 
			0.Go back to the Error Selection Menu 
	 		1.Invalid block number 
	 		2.Invalid packet header during transfer 
	 		3.Invalid packet size 
		Select option : 
		
		3.3.4.1. Please select how you would like to corrupt the ACK packet
	3.3.5. When option 3: DATA packet is selected, the following menu is prompted:
		----------------------
		| Data packet Menu |
		----------------------
		Please select which error to generate
		Options : 
	 		0.Go back to the Error Selection Menu 
	 		1.Invalid block number 
	 		2.Invalid packet header during transfer 
	 		3.Invalid packet size 
		Select option : 
		
		3.3.4.1. Please select how you would like to corrupt the DATA packet
	3.3.6. When option 4: ERROR packet is selected, the following menu is prompted:
		----------------------
		| Error packet Menu |
		----------------------
		Please select which error to generate
		Options : 
	 		0.Go back to the Error Selection Menu 
	 		1.Invalid error number 
	 		2.Invalid packet header during transfer 
		Select option : 

		3.3.4.1. Please select how you would like to corrupt the ERROR packet
   3.4. When option 2 : Unknown transfer ID is selected, the following menu is prompted:
	----------------------
	| Unknown TID Menu |
	----------------------
	Please select the block type to corrupt
	Options : 
	 	0.Go back to the Error Selection Menu 
	 	1.Initiate on ACK packet
	 	2.Initiate on DATA packet
	Select option :
	3.4.1. Please select option 0 to go back to the error selection menu
	3.4.2. When either option 1 or 2 is selected, it prompts the following: 
		Please enter the block number simulate error on:
		3.3.2.1. Please enter which ACK or DATA packet you would like to simulate an unknown TID error on
   3.5. When option 4 : Transmission Error is selected, the following menu is prompted:
	----------------------
	| Illegal TFTP Operation Menu |
	----------------------
	Please select the packet type to simulate on:
	Options : 
	 	0.Go back to the Error Selection Menu 
	 	1.First packet
	 	2.ACK packet
	 	3.DATA packet
	 	4.ERROR packet
	Select option : 
	3.5.1. Please select option 0 to go back to the error selection menu
	3.5.2. Please select either option 1; 2; 3 or 4 to create an illegal TFTP operation error on either the first packet (RRQ/WRQ);
	       ACK packet; DATA packet or an ERROR packet repectiveley.
	3.5.3. When any of options 1; 2; 3 or 4 is selected, the following menu is prompted:
		--------------------------------
		|   Select Transmission Error    |
		--------------------------------
		Options : 
	 		0. Go back to main menu
	 		1. Lose Packet
	 		2. Delay Packet
	 		3. Duplicate Packet
		Select option : 
		
		3.5.3.1. Please select option 0 to go back to the error selection menu
		3.5.3.2. When option 1: Lose Packet is selected, the following is prompted when option 2 (ACK packet) or option 3 
			 (DATA packet) is selected: 
			 Please enter the block number simulate error on:
			 Here, Please enter which ACK or DATA packet you would like to lose
		3.5.3.3. When option 1: Lose Packet is selected in the transmission error menu and when options 1 (First packet) and 
			 4 (ERROR packet) is selected, nothing is prompted and the error simulator waits for traffic.
		3.5.3.4. When option 2: Lose Packet is selected, the following is prompted:
			 How long do you want to delay a packet for (milliseconds)?
			 Here, Please eneter a delay time that is greate than 1050ms. Please note that 1000ms is just 1s.
		3.5.3.5. When option 3: Duplicate Packet is selected in the transmission error menu and when options 1 (First packet) and 
			 4 (ERROR packet) is selected, nothing is prompted and the error simulator waits for traffic.
		3.5.3.6. When option 3: Duplicate Packet is selected, the following is prompted when option 2 (ACK packet) or option 3 
			 (DATA packet) is selected: 
			 Please enter the block number simulate error on:
			 Here, Please enter which ACK or DATA packet you would like to duplicate

==============================================================================================================
General UI option selections for TFTPClient.java
--------------------------------------------------------------------------------------------------------------
1. Please select whether detailed information about the program's execution should be given (Verbose) or omitted (Silent)
      -------------------------------
      | Client Select Logging Level |
      -------------------------------
      Options : 
         1. Verbose
         2. Silent

2. Please enter the absolute path of the folder which has the files you want to write from the client to the server; when the 
   following is prompted: 
   Enter a directory to use as your default directory to write from: 

3. Please select Test to use the error simulator
      --------------------------------
      | Select Client operation Mode |
      --------------------------------
      Options : 
         1. Normal (No Error Simulator)
         2. Test (With Error Simulator)

4. Please enter a number to select an option will take you to a section where.
            ----------------------
            | Client Select Menu |
            ----------------------
            Options : 
                 1. Read File
                 2. Write File
                 3. Exit
	4.1. Selecting option 3 would shut-down the client

5. Please enter a file name when prompted:
   <TFTP Client> : Please enter file name:
	5.1. We have included some test files in the TestFiles/ directory. you can copy these files into your default directory 
		5.1.1. 512bytes.txt
    		5.1.2. lessthan512byte.txt
   		5.1.3. 513bytes.txt
    		5.1.4. 1025bytes.txt
6. Hit enter then you will see the file transfer happen
            
7. This will then loop back to the "Client Select Menu" shown in the point 4 above

==============================================================================================================
Testing Instructions:
--------------------------------------------------------------------------------------------------------------
[Note]: For testing all of the error cases, Please follow the general UI instructions above for all client, server and error simulator.

For I/O Errors, Please do the following:
[Note]: For testing the following errors, you don't need the error simulator and you should run the client in normal mode (step 4 in General UI option selections for TFTPClient.java)

[Error code 1]: File not found
--------------------------------------------------------------------------------------------------------------
1. On the client select menu: select (1) Read File
2. Enter a file name that does not exist in the "/TFTP-Server-Storage-Folder" 
Expected output: "The file name you entered [your file's name] cannot be found and it causes an error: FILE NOT FOUND"

[Error code 2]: Access Violation
--------------------------------------------------------------------------------------------------------------
Instructions to change the permissions of a file: 
1. Go to the "/TFTP-Server-Storage-Folder" under your home
2. Select a file to be tested and right click on it
3. Click on [Properties] in the bottom of the drop down list
4. Switch to the security tab on top
5. To change permissions click [Edit]
6. Select your own user name and deny a few or all of the permissions
7. Click [Apply] and press [OK] and press [OK] again to exit out of the preferences window
Console testing Instructions:
1. On the client select menu: select (1) Read File
2. Enter the name of the file whose permissions were changed
Expected output: "Access denied: You do not have permissions to access the file [name]: please change file permissions"

[Error code 3]: Disk full or allocation exceeded
--------------------------------------------------------------------------------------------------------------
fill up a usb to almost full and write a file to it such that somehwere in the middle of the tranfer the disk will become full
1. Get a USB and fill almost full 
2. Change the configurations home directory to be the drive letter of the USB 
   2.1 Go to Configurations.java in eclipse
   2.2 Go to Line 13 
   2.3 Replace USER_HOME = System.getProperty("user.home") with something that looks like this: USER_HOME = "M:". Here enter the Drive that represents your USB.
3. Write a file to the server that will cause the USB to reach capacity before the transfer is done. 
4. To test a disk full on the client side, free some space on the usb and attempt to read a file from the server folder that when transfering into the client folder,
   the USB will reach capacity mid transfer and fail.
Expected output: "File transfer failed"
         "Attempted allocation exceeds remaining disk space. (0 bytes remaining on the disk)"

[Error code 6]: File already exists
--------------------------------------------------------------------------------------------------------------
1. On the client select menu: select (2) Write File
2. Enter file path of the file to be written such that the file name already exists on the server 
3. Repeat steps 1 and 2 with the same file path
Expected output: "The file name you entered [your file's name] already exists and it causes an error: FILE DOES NOT EXIST"
==============================================================================================================

Responsibilities
--------------------------------------------------------------------------------------------------------------
See report
==============================================================================================================
Files included
--------------------------------------------------------------------------------------------------------------
/client
    + TFTPClient.java
/helpers
    + BufferPrinter.java
    + Conversion.java
    + FileStorageService.java
    + Keyboard.java
/Networking
    + ClientNetworking.java
    + ServerNetworking.java
    + TFTPNetworking.java
/packet
    + AckPacket.java
    + DataPacket.java
    + ErrorPacket.java
    + Packet.java
    + PacketFactory.java
    + ReadPacket.java
    + ReadWritePacket.java
    + WritePacket.java
/resource
    + Configurations.java
    + Strings.java
    + Tuple.java
    + UIStrings.java
/server
    + Callback.java
    + TFTPServer.java
    + TFTPService.java
/testbed
    + ErrorChecker.java
    + ErrorCodeSimulator.java
    + ErrorSimulatorServer.java
    + ErrorSimulatorService.java
    + TFTPErrorMessage.java
    + TFTPUserInterface.java
/testbed.errorcode
    + ErrorCodeFive.java
    + ErrorCodeFour.java
    + TransmissionConcurrentSend.java
    + TransmissionError.java
/types
    + ErrorType.java
    + InstanceType.java
    + Logger.java
    + ModeType.java
    + RequestType.java
    + DiskFullException.java
==============================================================================================================
END
