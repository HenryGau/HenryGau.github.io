The magic word in the X window system is DISPLAY. A display consists (simplified) of:

a keyboard,
a mouse
and a screen.
A display is managed by a server program, known as an X server. The server serves displaying capabilities to other programs that connect to it.

The remote server knows where it have to redirect the X network traffic via the definition of the DISPLAY environment variable which generally points to an X Display server located on your local computer.

The value of the display environment variable is:

hostname:D.S
where:

hostname is the name of the computer where the X server runs. An omitted hostname means the localhost.

D is a sequence number (usually 0). It can be varied if there are multiple displays connected to one computer.

S is the screen number. A display can actually have multiple screens. Usually there's only one screen though where 0 is the default.

Example of values

localhost:4
google.com:0
:0.0
hostname:D.S means screen S on display D of host hostname; the X server for this display is listening at TCP port 6000+D.

host/unix:D.S means screen S on display D of host host; the X server for this display is listening at UNIX domain socket /tmp/.X11-unix/XD (so it's only reachable from host).

:D.S is equivalent to host/unix:D.S, where host is the local hostname.

:0.0 means that we are talking about the first screen attached to your first display in your local host

Read more here and here and here.

From a X(7) man page:

From the user's perspective, every X server has a display name of the form:

hostname:displaynumber.screennumber

This information is used by the application to determine how it should connect to the server and which screen it should use by default (on displays with multiple monitors):

hostname The hostname specifies the name of the machine to which the display is physically connected. If the hostname is not given, the most efficient way of communicating to a server on the same machine will be used. displaynumber The phrase "display" is usually used to refer to collection of monitors that share a common keyboard and pointer (mouse, tablet, etc.). Most workstations tend to only have one keyboard, and therefore, only one display. Larger, multi-user systems, however, frequently have several displays so that more than one person can be doing graphics work at once. To avoid confusion, each display on a machine is assigned a display number (beginning at 0) when the X server for that display is started. The display number must always be given in a display name. screennumber Some displays share a single keyboard and pointer among two or more monitors. Since each monitor has its own set of windows, each screen is assigned a screen number (beginning at 0) when the X server for that display is started. If the screen number is not given, screen 0 will be used.