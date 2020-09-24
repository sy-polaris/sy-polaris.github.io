---
id: 2283
title: New PC Navtex USB NASA
date: 2016-07-29T18:28:09+02:00
author: polaris
layout: post
categories:
  - Senza categoria
---
Arrivato il nuovo PC Navtex PRO della NASA Marine.
![navtex](/foto/navtex.jpg)

NAVAREA III schedule: http://www.dxinfocentre.com/navtex.htm

Interface Specification for NASA Marine PC Navtex Pro

1 Electronic Interface

Power input: +10Volts to + 16Volts.
RS232 interface:
data format: 8 bits, 1 start bit, no parity, 1 stop bit.
Connector: 9-pin D-type socket mounted on the board.
pin 2: 38,400 Baud output from Engine to PC
pin 3: 38,400 Baud input to Engine from PC
pin 5: common (ground).
Amplitudes: standard PC RS232 (0 to 5V)

2 Power-up settings

On power-up, the unit selects the following default conditions:
Reception on 518kHz (channel A).
Internal clock OFF.
Timed channel switching OFF (no times set).

3 Data format (Stored Navtex Messages)

Navtex message storage is initiated within the PC Navtex Engine by receipt of the ZCZC sequence and terminated by the NNNN sequence. Every character between ZCZC and NNNN is stored, followed by a terminator sequence. Each stored and transmitted Navtex message begins with a “>“ character followed by the received message ID (even if faulty). The terminator sequence consists of a sequence followed by a lower case “a” or “b” to signify that the preceding message was received on 518kHz (“a”) or 490kHz (“b”), an ASCII number in the range 0 to 255 representing the number of Forward Error Corrections (FEC) made during reception of the message, and a final . Each complete message following that format is immediately transmitted to the RS232 interface and stored in on board memory for later recall on command by a PC.

If, following reception of a valid ZCZC sequence, a message is lost, or the NNNN terminator sequence is faulty, or a new ZCZC sequence is received before an NNNN sequence, the faulty message is not stored or transmitted to the PC.

4 Data format (PC to Engine)

Commands sent by the PC to the Engine are listed below. In all cases where more than one command is to be sent, the next command should not be sent until a response is received from the Engine signifying that the Engine has finished processing the previous command. The valid commands comprise the following types:

1.Select 518kHz (channel A):
send $A
2.Select 490kHz (channel B):
send $B
Sending either of the above commands stops timed channel switches so the unit remains in the selected channel. These commands are abbreviated versions of the channel switch commands as follows.

3.Select timed switches to 518kHz (channel A):
send $A,hhmm,hhmm
4.Select timed switches to 490kHz (channel B):
send $B,hhmm,hhmm
5.
&#8211; where hhmm defines the 24-hour time, between 0000 and 2359, at which a switch to channel A or B is to occur. If only one timed switch per day is required, send the same time in the two hhmm fields.Sending either of these commands establishes timed channel switches. If the clock has not been set, timed switching cannot (of course) occur. Any of the abopve commands trigger an acknowledgement string of ok.

5.Set the internal clock (24-hour mode):
send $C,hhmm
&#8211; where hhmm is the 24-hour time between 0000 and 2359. The clock starts when the command is received, and “ticks” once a minute thereafter. Sending this command does not establish timed switching, which is set up by the commands defined above. Note that, in addition to the “ok” response, this command also triggers an acknowledgement with the time set, and the A and B channel switching times.

6.Send all messages, oldest first:
send $S
7.Send software version number:
send $V
8.
5 Transmission priority (PC to Engine)

If the PC transmits a switch channel command to the Navtex PC Pro at the same time as it is receiving a message, the command will not be implemented in the Navtex PC Pro until after the completion of the present message. Any further commands will be ignored until the “ok” response is sent by the Engine.

6 Data format (Engine to PC)

The messages sent by the Navtex PC Pro shall comprise strings transmitted on the RS232 link at 38,400 Baud. There is an arbitrary delay between receipt of any command and issuing the response specified below if the Engine is busy with other activities (such as saving incoming messages, etc.). Communications from Engine to PC consist of:
1.A sign-on message sent on power-up as follows: “NASA Navtex PC Pro.Version: Annnn.n” (without the quotes), and where “Annnn.n” is a NASA Marine Ltd. in-house software version code.
2.Single complete Navtex messages transmitted immediately following receipt on the selected channel (a = 518kHz, b = 490kHz) as specified in section 3.
3.All stored messages, sent oldest first. The transmission of all available stored messages is terminated with the sequence“end” (N.B. lower case, without the quotes).
4.The message “ok“ (without the quotes) following any valid $A, $B, or $C command which has been successfully implemented. (Note the lower case “ok”.)
5.The software version number, having the format defined as part of the sign-on string in 6.1 following receipt of a $V command.
6.A message “Command not recognised.” (without the quotes) following receipt of an unrecognised command.
7.A message “No messages saved yet.” (without the quotes) if a Send All command (see above) is received before any messages have been stored.
