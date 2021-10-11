MOVED to https://git.interhacker.space/sammm/midiOSCesp.git

midiOSCesp v0.1
By Sam Neurohack


Forward incoming midi messages as OSC message (UDP) to micropython host to trigger hardware event. In example : noteon, noteoff lights on/off some leds connected to an ESP 8266.

Remember to edit netconf.py for network/OSC configuration.
In this early version you also need to edit in main.py :

	- On your midikeyboard the left key midi notenumber : i.e leftnote = 36 
	- motherip and motheroscport if you want some debug information.

Connect the led strip data line to D5 (GPIO 14)

How it works ?

* Computer side : List and hook to all midi devices (real or virtual). OSC commands generated from incoming midi messages :
	- /noteon midichannel, note, velocity
	- /noteoff midichannel, note
	- /rawcc midichannel, CCnumber, CCvalue
	- /clock
	- /start
	- /stop

* Micropython/ESP side :

	- interpret /noteon and /noteoff and switch one led in a led strip. Changing or adding functions to clock or other midi msg is easy, look lserver.py. 
	- ESP 8266 from https://www.wemos.cc/en/latest/d1/d1_mini_lite.html
	- Needs micropython firmware (select v1.13 with the right RAM amount): https://micropython.org/download/esp8266/
	- Flash firmware, upload python files, run files,... thonny IDE : https://thonny.org/
	- Great tutorials : https://randomnerdtutorials.com/getting-started-thonny-micropython-python-ide-esp32-esp8266/

* midi learning software :

	- This has been tested with Synthesia.
	- Synthesia/Neothesia hook to midi OUT ports to send light guidance and obviously midiOSCesp listen to INcoming events. So you need to create a virtual midi port will forward event sent to its OUT port and to its IN port.  https://help.ableton.com/hc/en-us/articles/209774225-How-to-setup-a-virtual-MIDI-bus


More soon...
