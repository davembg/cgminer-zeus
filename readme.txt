
========================================
building step(see cgminer's readme):

in building configration step, you just need to run:

autoreconf -fvi

CFLAGS="-O2" ./configure --enable-icarus

As the configure.ac is changed to support the ltc miner now.




=================================
execution  example:

cgminer.exe -o stratum+tcp://usa-1.liteguardian.com:3335 -u aaaa.256 -p x  --chips-count 256 --ltc-clk 300 -S //./COM4 



===================================
execution option readme:

--ltc-debug 
enable debug info output


--chips-count 16   
16 chips in one COM port

--ltc-clk  250
clock 250M

--nocheck-golden
init with no Golden number check

--nocheck-scrypt
Don't check the miner's result. 
Must set it on openwrt 703N version, as the scrypt.c calculates wrong on MIPS platform.

if you can't find the device in pi, you can try the following: (always from with --nocheck-golden if you still run into problems)
If cgminer can't find device, first you need to add a param:
--nocheck-golden
Then you need to check the device com port number and add it in the command line.

I only know how to get it on the openwrt platform.

In openwrt, we use "ls /dev" to get the port:
/dev/ttyUSB0 or /dev/ttyUSB1
and add the following in the command line:
-S /dev/ttyUSB0  -S /dev/ttyUSB1


Or for auto get it on Bash script:
DEVS=`find /dev/ -type c -name "ttyUSB*"  | sed 's/^/-S /' |  sed ':a;N;$!ba;s/\n/ /g'`
you then get DEVS == -S /dev/ttyUSB0  -S /dev/ttyUSB1

So the command line is something like:

cgminer --chips-count 128 --ltc-clk 300 -S /dev/ttyUSB0  -S /dev/ttyUSB1