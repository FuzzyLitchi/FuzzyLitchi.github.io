There exists a lot of tools to help you talk to devices using UART (aka Serial communication). Here are some that I recommend. 

RX/TX which one goes to which?

## Baud rate
You need to know how many symbols are sent per second. If you're not told what the baudrate is, you can usually just guess it. The most common are 9600 and 115200 (also written as 9.6kHz and 115.2kHz).

More are listed on this [Wikipedia page](https://en.wikipedia.org/wiki/Serial_port#Settings)

## Linux
Serial devices show up under `/dev/`, they're usually called `/dev/ttyACM0` or `/dev/ttyUSB0`. If you have multiple devices you will get different numbers than 0. Here is a neat command to list the serial devices you have available.
```
ls /dev/ | grep -E 'tty(ACM|USB)'
```

picocom is nice and simple.
```
picocom /dev/ttyACM1 -b 115200
```

You can also use screen or minicom, which are more common.
```
screen /dev/ttyACM1 115200
minicom -D /dev/ttyACM1 -b 115200
```

## Windows

[PuTTY](https://www.putty.org/) is a tool that can do serial communication on windows. It's also avai

## MacOS

I think you can do something similar to Linux but idk. Will update page ^.^