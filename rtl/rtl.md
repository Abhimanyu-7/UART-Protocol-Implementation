# RTL Design

This document provides a detailed overview of the RTL design of the UART implementation. The design is composed of four main modules:

* **`baudrate.v`**: This module generates the clock enable signals for the transmitter and receiver at the specified baud rate. The receiver clock is oversampled by 16x to improve noise immunity and ensure reliable data reception.
* **`transmitter.v`**: This module implements the UART transmitter using a finite state machine (FSM). The FSM has four states: IDLE, START, DATA, and STOP.
* **`receiver.v`**: This module implements the UART receiver using an FSM. The FSM has three states: START, DATA, and STOP. The receiver also includes logic for oversampling and start bit detection.
* **`uart_top.v`**: This module is the top-level wrapper that instantiates and connects the baud rate generator, transmitter, and receiver modules.

## Block Diagrams:

### Top module UART rtl netlist:
<img width="1851" height="811" alt="image" src="https://github.com/user-attachments/assets/72870433-de66-4114-ba92-b2c830f3f5f8" />

### Baudrate generator RTL Netlist:
<img width="1848" height="767" alt="image" src="https://github.com/user-attachments/assets/65999e09-e83c-49a4-980a-cb885e2aa6de" />

### Transmitter Tx Netlist:
<img width="1859" height="561" alt="image" src="https://github.com/user-attachments/assets/2a18d7d8-4cca-4b29-a06b-07e4a4708618" />

### Tx FSM:
<img width="784" height="253" alt="image" src="https://github.com/user-attachments/assets/c574ba8f-c059-4000-838e-1ef9f95c46e7" />

### Receiver Rx Netlist:
<img width="1864" height="647" alt="image" src="https://github.com/user-attachments/assets/2c3c2753-7651-4d5c-86b6-f0ca77bea5e9" />

### Rx FSM: 
<img width="634" height="243" alt="image" src="https://github.com/user-attachments/assets/0f833874-21c2-4391-9411-b39eb691fefb" />


