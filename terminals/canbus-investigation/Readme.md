```
MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMMMMMMMMMMMMWX00OkxxddcddxxkOO0XWMMMMMMMMMMMMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMMMMMMWXOxoc:c.;cccccc.ccccc:.:c:ldxOXMMMMMMMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMMMXkoc',ccccc:.:ccccc.ccccc.;cccc,'::cdOXMMMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMM0xc:cccc,':cccc::ccccccccccccccc:.;cccccc:lxXMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMNkl,',:ccccc;;ccccccccccccccccccccc::cccccc:,',:lOWMMMMMMMMMMMMM
MMMMMMMMMMMMNxccccc;';cccccccccccccccccccccccccccccccccc;':cccccckWMMMMMMMMMMM
MMMMMMMMMMNdcccccc:..;cccccccccccccccccccccccccccccccccccccccccccc:kWMMMMMMMMM
MMMMMMMMM0c,,,,:cccc;..;cccccccccccccccccccccccccccccccccccccc:,,,;:lKMMMMMMMM
MMMMMMMWd:cccc;:cccccc;..,cccccccccccccccccccccccccccccccccccc;:cccccckMMMMMMM
MMMMMMNlcccccccccccccccc:..,:ccccccccccccccccccccccccccccccccccccccccc:oWMMMMM
MMMMMNc,,,,,:ccccccccccccc:..':cccccccccccccccccccccccccccccccccc:,,,,,;oWMMMM
MMMMWoccccc::ccccccccccccccc:'.':cccccccccccccccccccccccccccccccc::ccccccxMMMM
MMMMkccccccccccccccccccccccccc:'..:cccccccccccccccccccccccccccccccccccccc:0MMM
MMMN::cccccccccccccccccccccccccc:'..:cccccccccccccccccccccccccccccccccccc:cWMM
MMMk,,,,,:cccccccccccccccccccccccc:,..;ccccccccccccccccccccccccccccc:,,,,,;0MM
MMMlccccccccccccccccccccccccccccccccc,.;cccccccccccccccccccccccccccccccccccdMM
MMW:ccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccclMM
MMWOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOO0MM
MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM

Welcome to the CAN bus terminal challenge!

In your home folder, there's a CAN bus capture from Santa's sleigh. Some of
the data has been cleaned up, so don't worry - it isn't too noisy. What you
will see is a record of the engine idling up and down. Also in the data are
a LOCK signal, an UNLOCK signal, and one more LOCK. Can you find the UNLOCK?
We'd like to encode another key mechanism.

Find the decimal portion of the timestamp of the UNLOCK code in candump.log
and submit it to ./runtoanswer!  (e.g., if the timestamp is 123456.112233,
please submit 112233)
```
```
<SNIP>
...
(1608926678.592863) vcan0 244#0000000193
(1608926678.604843) vcan0 244#0000000138
(1608926678.616971) vcan0 244#0000000166
(1608926678.629068) vcan0 244#0000000135
elf@a7dcdc935f5f:~$ cat candump.log | wc -l
1369

We have 1369 CAN log entries in the candump log, so lets get all the unique ids
```
```
elf@a7dcdc935f5f:~$ cat candump.log | cut -d " " -f3 | cut -d "#" -f1 | sort | uniq
188
19B
244
```
```
elf@a7dcdc935f5f:~$ cat candump.log | cut -d " " -f3 | cut -d "#" -f1 | grep 188 | wc -l
35 ---> Not of our interest as the total result is 35 and the program statement states that,
"a LOCK signal, an UNLOCK signal, and one more LOCK. Can you find the UNLOCK?"
```
```
elf@a7dcdc935f5f:~$ cat candump.log | cut -d " " -f3 | cut -d "#" -f1 | grep 19B | wc -l
3 --> Looks interesting , 3 results , can be one LOCK, an UNLOCK and one more LOCK, however lets check the 3rd CAN-ID one as well
```
```
elf@a7dcdc935f5f:~$ cat candump.log | cut -d " " -f3 | cut -d "#" -f1 | grep 244 | wc -l
1331 --> Thats too much, dont look like the CAN-ID we are interested 
```
```
elf@a7dcdc935f5f:~$ cat candump.log | cut -d " " -f3 | grep ^19B*
19B#000000000000
19B#00000F000000 -> Possibly UNLOCK
19B#000000000000
```
```
elf@a7dcdc935f5f:~$ cat candump.log | grep 19B#00000F000000
(1608926671.122520) vcan0 19B#00000F000000
elf@a7dcdc935f5f:~$ ./runtoanswer 122520
Your answer: 122520

Checking....
Your answer is correct!

elf@a7dcdc935f5f:~$ 
```
