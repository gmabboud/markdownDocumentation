# Information for the RaspPI Dashboard Testing Using LTE

## Login Info

Username: dashboard
Password: dashboard

## Notes

To power the pi through usb-c we must use a usba to usbc cuz of something about
the usb spec

Power over CAN so we can just turn on the fake car power supply to get
it all setup

In order to display the dashboard we use X11 window system. To switch
between the tty's (which here are are sometimes graphical displays) use
CTRL+ALT+F1 where F1 can be any of the F keys.

All AT commands are in the form of atcom AT???????\...

We have the *ME910C1-WW* module

*startx* command to start a new x11 server

*startx --- -nocursor* command to disable the cursor

NOTE I DID DELETE MODEMANAGER AS THE TUTORIAL INSTRUCTS

**Testing Network Setup:** Hook router up and send ethernet from the
router to the PI.

Connect to the dd-wrt network and now you can ssh into
dashboard@dashboard

**CTRL+D disconnects or command exit** on Pi keyboard

**Power Supply:** Turn power supply on, then use v-set on the channel
being used to 12v, and set i-set to 1A, then press the output on off
switch and everything should turn on.

When it doesnt turn off after you press it the first time

192.168.1.1

## SixFab Documentation

[Main documentation page](https://docs.sixfab.com/page/cellular-internet-connection-in-ecm-mode)

[Base hat documentation](https://docs.sixfab.com/docs/getting-started-with-base-hat-and-telit-le910c1-module)

[General tutorial page](https://docs.sixfab.com/page/tutorials)

[QMI interface setup](https://docs.sixfab.com/page/setting-up-a-data-connection-over-qmi-interface-using-libqmi)

[Troubleshooting steps](https://docs.sixfab.com/docs/raspberry-pi-3g-4g-lte-base-hat-troubleshooting)
