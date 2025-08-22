# Simulation

This document describes the simulation setup for the UART project. The simulation is performed using a Verilog testbench that implements a loopback test.

## Testbench

The testbench, `uart_TB.v`, instantiates the `uart` module and connects the `Tx` output to the `Rx` input, creating a loopback configuration. The testbench then transmits a sequence of data bytes and verifies that the received data matches the transmitted data.

The testbench also generates a VCD (Value Change Dump) file, `uart.vcd`, which can be used to visualize the simulation waveforms in a waveform viewer such as GTKWave.

## Waveforms:

The following waveform shows the transmission of the character 'A' (ASCII value 0x41) from the transmitter to the receiver.

As you can see from the waveform, the transmitter sends the start bit, followed by the 8 data bits (LSB first), and finally the stop bit. The receiver correctly receives the data and makes it available on the `data_out` port.

<img width="1887" height="888" alt="image" src="https://github.com/user-attachments/assets/c25e4d51-2bde-402a-9439-4e0eed7eb9c5" />
<img width="1880" height="876" alt="image" src="https://github.com/user-attachments/assets/26ffa1f1-f775-49ea-8f05-a9b4e30b9317" />
