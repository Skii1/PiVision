# RiseVisionPi
Open source edition of RiseVision ecosystem. Chrome Boxes are replaced with Raspberry Pi 4s, with ethernet, USB A ports, and a MicroSD card slot. Raspberry Pis connect to local server, and display content to the TVs, acting as an intermediate, or a buffer to output to the TVs (made by amateurs)!

sudo nano /etc/xdg/lxsession/LXDE-pi/autostart 

@xset s off
@xset -dpms
@xset s noblank
@chromium-browser --kiosk http://google.com/  # load chromium after boot and open the website in full screen mode

