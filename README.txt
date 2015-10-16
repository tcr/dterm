dterm: A simple terminal program


dterm is a simple terminal emulator, which doesn't actually emulate
any particular terminal.  Mainly, it is designed for use with xterm
and friends, which already do a perfectly good emulation, and therefore
don't need any special help; dterm simply provides a means by which 
keystrokes are forwarded to the serial line, and data forwarded from
the serial line appears on the terminal.


Running dterm

dterm is invoked thusly:

	dterm [options|device ...] 

dterm attempts to read the file ~/.dtermrc for options; if this doesn't
exist, it tries /etc/dtermrc.  Then it parses the options passed on the
command line.

The options read should include a device name, e.g "ttyS0" or "ttyd0"
for the first serial port on a Linux or FreeBSD system respectively.  If
no device is specified, dterm tries /dev/ttyS0, /dev/ttyd0, /dev/ttyUSB0
and /dev/ttyU0.

Once started, dterm can be got into command mode using Ctrl/].  Press
enter once from command mode to get back into conversational mode.  (The
command character can be changed with the esc= option, e.g. esc=p to 
use Ctrl/P instead of Ctrl/].)


Options

The following options can be used from command mode

- 300, 1200, 9600 etc: Set speed, default 9600.
- 5, 6, 7, 8: Set bits per character, default 8.
- 1, 2: Set number of stop bits, default 1.
- e, o, n, m, s: Set parity to even, odd, none, mark or space, default none.
- cts, nocts:  Enable / disable CTS flow control, default nocts.
- xon, noxon: Enable / disable XON/XOFF flow control, default noxon.
- modem: Enable / disable modem control (hang up modem on exit, exit if
modem hangs up), default nomodem.
- bs, nobs: Enable / disable mapping of Delete to Backspace, default nobs.
- del, nodel: Enable / disable mapping of Backspace to Delete, default nodel.
- maplf, nomaplf: Enable / disable mapping of LF to CR, default nomaplf.
- igncr, noigncr: Ignore / output carriage returns, default noigncr.
- crlf, nocrlf: Enable / disable sending LF after each CR, default nocrlf.
- ctrl, noctrl: Enable / disable control character display mode.  In this
mode, non-printable characters are displayed as ^c for the codes 0-31 (except
CR, LF & TAB), [DEL] for 127, or [xx] for non-printing characters >= 128.
- hex, nohex: As for ctrl, but prints [xx] for all characters except 7-bit
printable ASCII, CR and LF.
- b: Send a 500 ms break.
- dtr, nodtr: Raise / lower DTR, default dtr.
- rts, norts: Raise / lower RTS, default rts.
- d, r: Toggle DTR / RTS.
- esc=<c>: Set command mode character to Ctrl/<c> (default ']') 
- @<filename>: Read and process configuration from <filename>.
- !<command>: Execute shell command
- sx <filename>: Send a file using XMODEM.
- rx <filename>: Receive a file using XMODEM.
- sz <filename>: Send a file using ZMODEM.
- rz: Receive file(s) using ZMODEM.
- show: Display current configuration and modem status.
- help, h, ?: Display a summary of commands.
- version: Display version, copyright and warranty information.
- quit, q: Exit


File Transfer

If the rzsz package (or lrzsz) package is installed, the sx, sz, rx & rz
commands can be used to initiate file transfers using the reliable
XMODEM and ZMODEM file transfer protocols.  Note that the program files
for rzsz must be in /usr/bin or /usr/local/bin for dterm to find them.

Note that rx, sx and rz require that the transfer be initiated at the
remote end before escaping back to the dterm command prompt.  sz will send 
an "rz" command down the serial link in start-up to initiate the transfer.


Examples

Connect via ttyS1 to a system running at 2400 bps, 7 bits even parity:

	dterm ttyS1 2400 7 e

Send a break in a running session:

	^]
	dterm> b
	dterm>

Transmit a file using ZMODEM:

	^]
	dterm> sz file.txt
	rz waiting to receive.Sending: file.txt
	Bytes Sent:  22943   BPS:645                             
	Transfer complete
	dterm>


Copyright

dterm is Copyright 2007 Knossos Networks Ltd.

This program is free software; you can redistribute it and/or
modify it under the terms of the GNU General Public License version 2
as published by the Free Software Foundation.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

A copy of the GNU General Public License version 2 is available at
http://www.knossos.net.nz/gpl.html or can be obtained from the Free
Software Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA
02110-1301 USA.


Source Code

dterm source code is located at 
http://www.knossos.net.nz/downloads/dterm-0.3.tgz

