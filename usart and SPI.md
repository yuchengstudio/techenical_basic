# reference
https://www.edaboard.com/showthread.php?69740-Difference-between-USART-and-SPI

# 
The Serial Peripheral Interface Bus or SPI (often pronounced like "spy") bus is a very loose standard for controlling almost any digital electronics that accepts a clocked serial stream of bits. A nearly identical standard called "Microwire" is a restricted subset of SPI.

SPI is cheap, in that it does not take up much space on an integrated circuit, and effectively multiplies the pins, the expensive part of the IC. It can also be implemented in software with a few standard IO pins of a microcontroller.

Many real digital systems have peripherals that need to exist, but need not be fast. The advantage of a serial bus is that it minimizes the number of conductors, pins, and the size of the package of an integrated circuit. This reduces the cost of making, assembling and testing the electronics.

A serial peripheral bus is the most flexible choice when many different types of serial peripherals must be present, and there is a single controller. It operates in full duplex (sending and receiving at the same time), making it an excellent choice for some data transmission systems.

In operation, there is a clock, a "data in", a "data out", and a "chip select" for each integrated circuit that is to be controlled. Almost any serial digital device can be controlled with this combination of signals.

SPI signals are named as follows:

* SCLK - serial clock
* MISO - master input, slave output
* MOSI - master output, slave input
* CS - chip select (optional, usually inverted polarity)

Most often, data goes into an SPI peripheral when the clock goes low, and comes out when the clock goes high. Usually, a peripheral is selected when chip select is low. Most devices have outputs that become high impedance (switched-off) when the device is not selected. This arrangement permits several devices to talk to a single input. Clock speeds range from several thousand clocks per second (usually for software-based implementations), to over 10 million per second.

Most SPI implementations clock data out of the device as data is clocked in. Some devices use that trait to implement an efficient, high-speed full-duplex data stream for applications such as digital audio, digital signal processing, or full-duplex telecommunications channels.

On many devices, the "clocked-out" data is the data last used to program the device. Read-back is a helpful built-in-self-test, often used for high-reliability systems such as avionics or medical systems.

In practice, many devices have exceptions. Some read data as the clock goes up (leading edge), others read as it goes down (falling edge). Writing is almost always on clock movement that goes the opposite direction of reading. Some devices have two clocks, one to "capture" or "display" data, and another to clock it into the device. In practice, many of these "capture clocks" can be run from the chip select. Chip selects can be either selected high, or selected low. Many devices are designed to be daisy-chained into long chains of identical devices.

SPI looks at first like a non-standard. However, many programmers that develop embedded systems have a software module somewhere in their past that drives such a bus from a few general-purpose I/O pins, often with the ability to run different clock polarities, select polarities and clock edges for different devices.

The interface is also easy to implement for bench test equipment. For example, the classic way to implement an SPI interface from a personal computer to custom electronics is via a custom cable to the PC's parallel printer port. The parallel port generates and reads standard TTL logic voltages; +5V is high, ground is low. A number of helpful people have developed drivers to give access to this port in the most restrictive operating systems, such as Windows NT (see below), from the least likely environments, such as Visual Basic.

In some organizations, these pieces of code have become quite stylized and generalized. Often the serial bus passes through a programmable logic array, making the hardware programmable, as well as the software (see JTAG).

Motorola actually developed a standard microcontroller peripheral for these sorts of buses, which gave them a name









    A UART or Universal Asynchronous Receiver-Transmitter is a piece of computer hardware that translates between parallel bits of data and serial bits. A UART is usually an integrated circuit used for serial communications over a computer or peripheral device serial port. UARTs are now built into some microcontrollers (for example, PIC16F628).
    Contents
    [hide]

    * 1 Basics
    * 2 Components of a typical UART chip
    * 3 Error conditions
    o 3.1 Overrun Error
    o 3.2 Framing Error
    o 3.3 Parity Error
    o 3.4 Break Error
    * 4 Synchronous
    * 5 History
    * 6 See also

    [edit]

    Basics

    Bits have to be moved from one place to another using wires or some other medium. Over many miles, the expense of the wires becomes large. To reduce the expense of long communication links carrying several bits in parallel, data bits are sent sequentially, one after another, using a UART to convert the transmitted bits between sequential and parallel form at each end of the link. Each UART contains a shift register which is the fundamental method of conversion between serial and parallel forms.

    By convention, teletype-style UARTs send a "start" bit, five to eight data bits, least-significant-bit first, an optional "parity" bit, and then a "stop" bit. The start bit is the opposite polarity of the data-line's normal state. The stop-bit is the data-line's normal state, and provides a space before the next character can start. In mechanical teletypes, the "stop" bit was often stretched to two bit times to give the mechanism more time to finish printing a character. A stretched "stop" bit also helps resynchronization. The parity bit can either make the number of bits odd, or even, or it can be omitted. Odd parity is more reliable because it assures that there will always be a data transition, and this permits many UARTs to resynchronize.

    Speeds for UARTs are in bits per second (bit/s or bps), although often incorrectly called the baud rate. Standard mechanical teletype rates are 45.5, 110, and 150 bit/s. Computers have used from 110 to 230,400 bit/s. Standard speeds are 110, 300, 1200, 2400, 4800, 9600, 19,200, 28,800, 38,400, 57,600, and 115,200 bit/s.

    The UART usually does not directly generate or receive the voltage levels that are put onto the wires interconnecting different equipment. An interface standard is used, which defines voltage levels and other characteristics of the interconnection. Examples of interface standards are EIA, RS 232, RS 422 and RS 485. Depending on the limits of the communication channel to which the UART is ultimately connected, communication may be "full duplex" (both send and receive at the same time) or "half duplex" (devices take turns transmitting and receiving). Beside traditional wires, the UART is used for communication over other serial channels such as an optical fiber, infrared, wireless Bluetooth in its Serial Port Profile (SPP) and the DC-LIN for power line communication.

    Today (2006), UART is commonly used with RS232 for embedded systems communications. It is useful to communicate between microcontrollers and also with PCs. Many chips provide UART functionality in silicon, and low cost chips exist to convert UART to RS232 signals (for example, Maxim MAX232).
    [edit]

    Components of a typical UART chip

    A UART chip usually contains the following components:

    * Transmit/Receive Buffer

    * Transmit/Receive Control

    * Data Bus Buffer

    * Read/Write Control Logic

    * Modem Control

    [edit]

    Error conditions
    [edit]

    Overrun Error

    A possible failure of a UART occurs when it cannot process the byte that just came in before the next one arrives. Various UART devices have differing amounts of buffer space to hold received characters. The CPU must service the UART in order to remove characters from the buffer. If the CPU does not service the UART and the buffer becomes full, Overrun Error will occur.
    [edit]

    Framing Error

    Another possible error occurs when the designated "start" and "stop" bits are not valid. As the "start" bit is used to identify the beginning of an incoming character, it acts as a reference for the remaining bits. If the data line is not in its normal state when the "stop" bit is expected, a Framing Error will occur.
    [edit]

    Parity Error

    The third possible error condition occurs when the number of "active" bits does not agree with the specified parity configuration of the UART, producing a Parity Error. Because the "parity" bit is optional, this error will not occur if parity has been disabled.
    [edit]

    Break Error

    The final possible error is the break error. This occurs when the connection is broken, It is detected when the transmission line does not send the stop bit.
    [edit]

    Synchronous

    The word "asynchronous" indicates that UARTs recover character timing information from the data stream, using designated "start" and "stop" bits to indicate the framing of each character. In synchronous transmission, the clock data is recovered separately from the data stream and no start/stop bits are used. This improves the efficiency of transmission on suitable channels; more of the bits sent are data. An asynchronous transmission sends nothing over the interconnection when the transmitting device has nothing to send; but a synchronous interface must send "pad" characters to maintain synchronism between the receiver and transmitter. The usual filler is the ASCII "SYN" character. This may be done automatically by the transmitting device.

    Some chips have both synchronous and asynchronous modes. These are called USARTs (for "universal synchronous asynchronous receiver-transmitters").
    [edit]

    History

    The first UART-like devices were rotating mechanical commutators. These sent 5-bit baudot codes for mechanical teletypewriters, and replaced morse code. Later, ASCII required a seven bit code. When IBM rationalized computers in the early 1960s with 8-bit characters, it became customary to store the ASCII code in 8 bits.

    Gordon Bell designed the first UART for the PDP-1.

    An example of an early 1980s UART was the National Semiconductor 8250. In the 1990s, newer UARTs were developed with on-chip buffers. This allowed higher transmission speed without data loss and without requiring such frequent attention from the computer. For example, the National Semiconductor 16550 has a 16 byte FIFO. Variants include the 16C550, 16C650, 16C750, and 16C850.

    Depending on the manufacturer, different terms are used to identify devices that perform the UART functions. Intel called their 8251 device a "Programmable Communication Interface". The term "Serial Communications Interface" (SCI) was first used at Motorola around 1975 to refer to their start-stop asynchronous serial interface device, which others were calling a UART.

    The less-common 5, 6 and 7 bit codes are now sometimes simulated with 8-bit UARTs. The unused high-order bits are set to 1, the value of the stop bit and idle line. This technique cannot send or receive at full speed, but provides some level of compatibility for older equipment.

    Some very low-cost home computers or embedded systems dispensed with a UART and used the CPU to sample the state of an input port or directly manipulate an output port for data transmission. While very CPU-intensive, since the CPU timing was critical, these schemes avoided the purchase of a costly UART chip. The technique was known as a bit-banging serial port.

    UART is also playing a significant role in the advancement of wireless communications protocols.
