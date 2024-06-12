## PiVision ##
Open source edition of RiseVision ecosystem. Chrome Boxes are replaced with Raspberry Pi 4s, with ethernet, USB A ports, and a MicroSD card slot. Raspberry Pis run on a scheduled runtime and dispay any webpage or app on startup.

Instructions and documentation can be found on our User Documentation here :

Or, a more technical and specific documntation for anyone modifying the system scripts is in the "README" in the repo files, and specific instructions to the autostart and CRON scheduler process.

# Breakdown #

The system is relativley simple, with most of the issues during implementation origination from corperate domains blocking the NTP service. An ethernet connection is recommended, with "rfkill" enabled on your wireless network adapter. An alternate DNS is also highly recommended, such as "8.8.8.8" and "8.0.0.8".

### Autostart ###

An autostart program can be implemented in a few ways, but the most foolproof way to do it is to create a script in the directory "~/.config/lxsession/LXDE-pi/".
This script will run immediatley on start up because it targets the desktop session. Once the desktop initializes, the script is executed thereafter.

### Cronscripts ###

Scripts in this folder are executed through the CRON task scheduler. Cron tasks can implemented in specfied minutes, hours, days, day of month, month, and day of week. You can set values to specific minutes of the hour, such as 'on every 5th minute of the hour' or, periodically, such as 'on every 5th minute'. Find more information about the CRON task scheduler in the link here:

### Webpage ###

The webpage for our specific use case is a free domain with a small date/time widget, along with google slides and google calendar implementations. Most of the editable data is in the google slides/calendar, as it is automatically updated with all changes made by our organization, and editing the webpage data seperatley is not required. 

## How it works ##

On startup, the desktop environment initializes. During this process, the scripts in the LXDE environment folder are called, such as the 'autostart' script. The autostart script disables the splash screen and popups in a new chromium session with a specified link to open. Ideally, a 'kiosk mode' flag should be added to lock the browser, so that no one can change the tab or tamper with the system.

In the background, the CRON task scheduler is running, and periodically running scripts. One of the flaws of using a free domain is not being able to get live updates. If someone makes an update on the server, the information won't display, as the page needs to be refreshed, and the browser cache needs to be cleared. First, 'dropcache.sh' deletes everything in the chromium cache folder. Directly after, 'refresh.sh' is run which refreshes the browser using 'xdotools', a package that allows key macros to be executed in a shell scripts. In this case, "Ctrl + F5". This cycle will be repeated in the CRON scheduler indefinitely, on a set interval. 

Once the display no longer needs to be enabled, another CRON task runs, which forciibly turns off the display.

Note : the display will still be "turned on", but the Pi will stop sending information to the display, in a sort of sleep mode. It can be woken up by entering any input.

Since the Pi is still technically running, all the CRON scripts are aswell. Once the display is required again, it will forcibly enable the display.

## DISCLAIMER ##

Being open source, and done for a project, there is no guaruntee this software will be activley maintained. It is encouraged that someone technically knowledgeable maintains the system for individual users.

