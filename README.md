# UART-Protocol-Implementation
A verilog implementation of UART Communication protocol


## Project Structure
```
uart_project/
├── rtl/
│   ├── uart_tx.v               # UART Transmitter (FSM-based)
│   ├── uart_rx.v               # UART Receiver (FSM-based)
│   ├── baud_gen.v              # Baud rate generator (tick for bit sampling)
│   └── uart_top.v              # Wrapper to connect Rx, Tx, and Baud
│
├── sim/
│   ├── uart_tb.v               # Full testbench for simulation
│   └── waveforms   # Optional: loopback test
│
├── definitions.vh              # defining Macros
│
└── README.md                   # Design explanation
```

## ✅ Features 

- **Parametrized Baud Generator**
- **Tx FSM**: start bit → 8 data bits → stop bit

- **Rx FSM**: sync start → sample → shift into byte

- **Loopback test** (Tx → Rx connection)

- **Testbench** to send/receive characters

## UART Basics
+ UART, or `Universal Asynchronous Receiver-Transmitter`, is a hardware communication protocol that uses asynchronous serial communication with configurable speed. 
          
+ *Asynchronous* means there is **no clock signal** to synchronize the output bits from the transmitting device going to the receiving end.

### Interface

<p align="center"> <img width="655" height="190" alt="image" src="https://github.com/user-attachments/assets/2f135865-e5ef-4443-9a55-0248701b85c0" /></p>

- The two signals of each UART device are named:

  - Transmitter (Tx)
  - Receiver (Rx)

>
>The main purpose of a transmitter and receiver line for each device is to transmit and receive serial data intended for serial communication.


### UART with data bus
<p align="center> <img width="655" height="304" alt="image" src="https://github.com/user-attachments/assets/c4a5d468-aa5c-4c82-8bce-b752663fbe85" /></p>

1. The transmitting UART is connected to a controlling data bus that sends data in a parallel form. From this, the data will now be transmitted on the transmission line (wire) serially, bit by bit, to the receiving UART. This, in turn, will convert the serial data into parallel for the receiving device.
2. The UART interface does not use a clock signal to synchronize the transmitter and receiver devices; it transmits data asynchronously. Instead of a clock signal, the transmitter generates a bitstream based on its clock signal while the receiver is using its internal clock signal to sample the incoming data.

### Baud Rate

`Baud Rate` refers to the rate at which data is transmitted between devices, specifically the number of signal changes (or symbols)  transmitted per second. It essentially dictates the speed at which bits are sent over the communication  link. 

> A **higher** baud rate means **faster** data transmission

## UART Packet

<p align="center"> <img width="875" height="91" alt="image" src="https://github.com/user-attachments/assets/fd64d61a-2f46-4cd0-a3dc-b028e18e6ae7" /></p>

> ### Start Bit
The UART data transmission line is normally held at a high voltage level when it’s not transmitting data. To start the transfer of data, the transmitting UART pulls the transmission line from high to low for one (1) clock cycle. When the receiving UART detects the high to low voltage transition, it begins reading the bits in the data frame at the frequency of the baud rate.

> ### Data Frame
The data frame contains the actual data being transferred. It can be five (5) bits up to eight (8) bits long if a parity bit is used. If no parity bit is used, the data frame can be nine (9) bits long. In most cases, the data is sent with the least significant bit first.

> ### Parity Bit
Parity describes the evenness or oddness of a number. The parity bit is a way for the receiving UART to tell if any data has changed during transmission. 

> [!NOTE]
> Bits can be changed by **electromagnetic radiation** , **mismatched baud rates** , or **long-distance data transfers**.

> ### Stop Bit
To signal the end of the data packet, the sending UART drives the data transmission line from a low voltage to a high voltage for one (1) to two (2) bit(s) duration.


## Steps of UART Transmission
### Step 1: 
The transmitting UART receives data in parallel from the data bus.
<p align = "center" ><img width="497" height="537" alt="image" src="https://github.com/user-attachments/assets/d2417802-5b9d-43d3-9aa6-f9e489a6009e" /></p>

### Step 2:
The transmitting UART adds the start bit, parity bit, and the stop bit(s) to the data frame.
<p align="center"><img width="541" height="321" alt="image" src="https://github.com/user-attachments/assets/d57b8574-842a-43ee-9c44-c117a3346829" /></p>

### Step 3:
The entire packet is sent serially starting from start bit to stop bit from the transmitting UART to the receiving UART. The receiving UART samples the data line at the preconfigured baud rate.
<p align="center"><img width="654" height="308" alt="image" src="https://github.com/user-attachments/assets/6f6c20ef-35a2-4f0a-8aa3-3e7e99917232" /> </p>

### Step 4:
The receiving UART discards the start bit, parity bit, and stop bit from the data frame.
<p align="center"><img width="541" height="321" alt="image" src="https://github.com/user-attachments/assets/b0cf96df-0dfb-4b17-a814-6167b71f1e6e" />
</p>
### Step 5:
The receiving UART converts the serial data back into parallel and transfers it to the data bus on the receiving end.
<p align="center"><img width="477" height="537" alt="image" src="https://github.com/user-attachments/assets/07b95262-ba0a-4e4f-9ff3-99a042d895a6" />
</p>


