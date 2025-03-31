# 📡 Minitalk - UNIX Signal Communication

Welcome to my **Minitalk** repository! This project is part of the **42 curriculum**, where I implemented a simple client-server communication system using UNIX signals. This project deepened my understanding of UNIX signals, bit manipulation, and process communication in C.

---

## **✅ Project Validation**
- **Validated on:** September 12, 2024
- **Final Score:** 105/100

---

## **📜 Project Overview**
The goal of this project was to create a communication program between a client and server using exclusively UNIX signals. The client sends a string to the server, which then displays it. This implementation demonstrates understanding of process communication, signal handling, and binary data transmission.

### **Key Requirements:**
- Create client and server executables
- Server prints its PID on startup
- Client accepts server PID and string to send as parameters
- All communication must use only UNIX signals (SIGUSR1 and SIGUSR2)
- Server must display received strings promptly
- Server should handle multiple clients without needing to restart

### **Restrictions:**
- The project had to be coded in C
- Limited to using only certain functions:
  - write, signal, sigemptyset, sigaddset, sigaction, kill
  - getpid, malloc, free, pause, sleep, usleep, exit
  - My own printf

---

## **🛠️ Implementation Details**

### **🔄 Signal Communication**
- Used **SIGUSR1** and **SIGUSR2** for binary data transmission
- **SIGUSR1** represents bit '0'
- **SIGUSR2** represents bit '1'
- Each character is transmitted bit by bit (8 bits per character)
- Includes proper signal handling with sigaction

### **🖥️ Server Implementation**
- Prints its PID on startup for client connection
- Sets up signal handlers for SIGUSR1 and SIGUSR2
- Reconstructs characters from received bits
- Prints characters as they are completed
- Handles multiple clients sequentially

### **💻 Client Implementation**
- Takes server PID and message string as arguments
- Converts each character to binary representation
- Sends each bit as a signal to the server
- Properly handles transmission of entire strings

### **⚙️ Error Handling**
- Validates command-line arguments
- Checks for valid PIDs
- Ensures proper signal transmission
- Handles edge cases gracefully

---

## **📂 Project Structure**
```
minitalk/
│── minitalk.h             # Header file with function prototypes and includes
│── printf/                # Custom printf implementation
│   │── ft_print_charstr.c
│   │── ft_print_hexa.c
│   │── ft_print_int.c
│   │── ft_print_percent.c
│   │── ft_print_ptr.c
│   │── ft_print_unsigned.c
│   │── ft_printf.c
│   │── ft_printf.h
│   └── Makefile
│── src/                   # Source files
│   │── client.c           # Client implementation
│   └── server.c           # Server implementation
└── Makefile               # Main compilation instructions
```

---

## **🔧 Installation & Usage**

### **📋 System Requirements**
- UNIX-based operating system (Linux/macOS)
- C compiler (gcc/cc)

### **📥 Clone & Compile**
```
# Clone the repository
git clone https://github.com/osmaneb23/42-Minitalk.git
cd 42-Minitalk

# Compile the project
make
```

The Makefile handles all necessary compilation steps, including:
- Compiling the custom printf library
- Compiling the server and client executables
- Ensuring proper linking

### **🚀 Running the Program**

#### **1. Start the server**
```
# Run the server first
./server
```

The server will display its PID, which is needed for the client to connect.

#### **2. Send a message from the client**
```
# Run the client with server PID and message
./client [server_pid] "Your message here"
```

Example:
```
./client 4567 "Hello from Minitalk!"
```

#### **3. Expected Output**
On the server terminal, you should see the received message displayed promptly.

---

## **🔬 How It Works**

### **Binary Communication**
The client and server communicate using binary encoding:
1. Client converts each character to its 8-bit binary representation
2. For each bit in the binary representation:
   - Sends SIGUSR1 for bit value '0'
   - Sends SIGUSR2 for bit value '1'
3. Server receives these signals and reconstructs the original character
4. After reconstructing, server displays the character immediately

### **Signal Handling Flow**
1. Server registers signal handlers using sigaction()
2. Client sends signals using kill()
3. Server's signal handler processes signals as they arrive
4. Server accumulates bits until a full character is received (8 bits)
5. When a character is complete, it's displayed with write() or ft_printf()
6. Process continues for each character in the message

---

## **🎮 Example Usage**

Terminal 1 (Server):
```
``` ./server
Server PID: 4567
Waiting for signals...
Hello from Minitalk!
```

Terminal 2 (Client):
```
``` ./client 4567 "Hello from Minitalk!"
Message sent successfully!
```

---

## **⚠️ Error Handling**
The program provides helpful error messages for various scenarios:
- Invalid server PID
- Invalid arguments
- Signal transmission failures

---

## **🎓 Key Learning Outcomes**
- **UNIX Signals:** Understanding and implementing signal handling (SIGUSR1, SIGUSR2)
- **Process Communication:** Inter-process communication techniques
- **Bit Manipulation:** Converting characters to bits and vice versa
- **Signal Handling:** Using sigaction() for robust signal handling
- **Binary Encoding:** Implementing binary data transmission protocols
- **Error Management:** Proper error handling in client-server communications
- **Makefile Management:** Creating and structuring makefiles for multi-component projects
- **Process Management:** Working with process IDs and process interactions
- **Timing & Synchronization:** Handling transmission timing between processes