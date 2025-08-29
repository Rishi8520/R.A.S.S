🚀 Project Overview

R.A.S.S - An Embedded Web Server

R.A.S.S stands for Rishi, Anirudh, Sumedh and Swaminath, is a project that implements a complete embedded web server solution that enables IoT functionality for ARM-based embedded systems. The system combines hardware-level Ethernet communication with a robust web server framework to provide real-time sensor monitoring and control capabilities.
Key Features

    Hardware Platform: LPC2148 ARM7TDMI-S microcontroller

    Ethernet Connectivity: ENC28J60 SPI-to-Ethernet controller

    Web Framework: Mongoose embedded web server library

    Real-time Data: Simulated sensor data (temperature, humidity, pressure, light)

    Web Interface: Flask-based frontend with MySQL database integration

    Cross-platform Support: Windows DLL integration for extended functionality


🔧 Hardware Configuration
LPC2148 ARM7 Microcontroller

    Architecture: ARM7TDMI-S 32-bit RISC core

    Flash Memory: 512KB

    RAM: 42KB (32KB + 8KB + 2KB)

    Operating Frequency: Up to 60MHz

    Peripherals: SPI, UART, GPIO, Timers

ENC28J60 Ethernet Controller

    Interface: SPI communication

    Speed: 10BASE-T Ethernet

    Buffer: 8KB transmit/receive buffer

    Pin Connections:

        CS: P0.10

        SCK: P0.4

        MOSI: P0.5

        MISO: P0.6

💻 Software Architecture
Core Components
1. Main Application (main.c)

c
// Key functionalities:
- SPI communication setup
- ENC28J60 initialization  
- Mongoose web server integration
- Sensor data generation and JSON conversion
- HTTP request handling
- Real-time data streaming

2. ENC28J60 Driver (ENC28J60_driver.c)

c
// Driver capabilities:
- SPI protocol implementation
- Ethernet controller configuration
- Packet transmission/reception
- Network buffer management
- MAC address configuration

3. Sensor Data Management (Sensor_rand.c, sensorData.h)

c
typedef struct {
    double temperature;  // °C
    double humidity;     // %
    double pressure;     // hPa  
    double light;        // lux
} SensorData;

4. Web Interface (FRONTEND/app.py)

    Framework: Flask web application

    Database: MySQL integration for data logging

    Features:

        Real-time sensor data display

        Historical data visualization

        REST API endpoints (/api/current, /api/historical)

        Background data collection threading

Network Configuration

c
// Default network settings
IP Address: 192.168.1.100
MAC Address: 00:12:34:56:78:9A
Web Server Port: 80
Database: MySQL (sensor_data_db)

🌐 Web Interface Features
Dashboard (R.A.S.S.)

    Real-time sensor monitoring

    Temperature, voltage, pressure, and magnetic field readings

    Auto-updating display with visual indicators

    Navigation menu for different system functions

API Endpoints
Endpoint	Method	Description
/	GET	Main dashboard interface
/api/sensor	GET	Current sensor data (JSON)
/api/current	GET	Real-time data via Flask
/api/historical	GET	Historical data from database
Database Schema

sql
CREATE TABLE SensorData (
    id INT AUTO_INCREMENT PRIMARY KEY,
    temperature DOUBLE,
    humidity DOUBLE, 
    pressure DOUBLE,
    light DOUBLE,
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

🛠️ Build System
Keil µVision Project

    Project files: SERVER.uvproj, SERVER.uvopt

    Linker script: lpc2148_flash.ld

    Startup code: Startup.s

    Build output: SERVER.hex

CMake Support

    CMakeLists.txt for cross-platform building

    Supports both ARM and x86 compilation

    Integrated library generation

📚 Documentation

The PPTs & DOCs/ directory contains comprehensive project documentation:

    Datasheets: LPC2148 and ENC28J60 technical specifications

    Research Papers: Related embedded web server implementations

    Presentations: Project development milestones

    Reports: Detailed system design and implementation

    System Architecture: Visual system overview

🚀 Getting Started
Prerequisites

bash
# Hardware
- LPC2148 development board
- ENC28J60 Ethernet module  
- SPI connections
- Power supply (3.3V/5V)

# Software
- Keil µVision IDE
- Python 3.x with Flask
- MySQL database
- Cross-compilation toolchain (optional)

Hardware Setup

    Connect ENC28J60 to LPC2148 via SPI interface

    Wire power and ground connections

    Connect Ethernet cable to network

    Program LPC2148 with compiled firmware

Software Deployment

    Embedded System:

bash
# Compile with Keil µVision or CMake
# Flash SERVER.hex to LPC2148

Web Interface:

bash
cd FRONTEND/
pip install flask mysql-connector-python requests
python app.py
# Access dashboard at http://localhost:5000

Database Setup:

    sql
    CREATE DATABASE sensor_data_db;
    -- Configure credentials in app.py

🔬 Technical Specifications
Performance Metrics

    Web Response Time: < 100ms for sensor data requests

    Data Update Rate: 1Hz (configurable)

    Memory Usage: ~40KB RAM, ~200KB Flash

    Network Throughput: 10Mbps Ethernet capability

    Concurrent Connections: Limited by RAM (typically 2-4)

Supported Protocols

    HTTP/1.1: Web server and REST API

    TCP/IP: Network communication stack

    JSON: Data serialization format

    SPI: Hardware communication protocol

🔧 Configuration Options
Network Settings

c
// Modify in main.c
#define SERVER_IP "192.168.1.100"
#define SERVER_PORT 80
#define MAC_ADDR {0x00, 0x12, 0x34, 0x56, 0x78, 0x9A}

Sensor Simulation

c
// Adjust ranges in Sensor_rand.c
Temperature: 20.0°C - 30.0°C
Humidity: 40.0% - 60.0%  
Pressure: 950.0hPa - 1050.0hPa
Light: 100.0lux - 1000.0lux

🤝 Contributing

This project serves as a reference implementation for embedded web servers. Key areas for enhancement:

    Addition

    d security features

    Real-time graphing capabilities

    Mobile-responsive interface

    MQTT protocol support


🎯 Applications
Industrial IoT

    Remote equipment monitoring

    Environmental sensing

    Process control interfaces

    Data logging systems

Educational Use

    Embedded systems curriculum

    IoT development training

    Network programming concepts

    Real-time systems design

Research Applications

    Sensor network prototyping

    Communication protocol testing

    Performance benchmarking

    System integration studies

📞 Support

For technical questions or contributions:

    Review the comprehensive documentation in PPTs & DOCs/

    Examine source code comments and structure

    Reference Mongoose library documentation

    Consider hardware limitations and SPI timing requirements

Note: This is an educational/research project demonstrating embedded web server concepts. For production use, additional security, error handling, and optimization would be required.
