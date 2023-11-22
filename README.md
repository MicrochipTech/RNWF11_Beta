# RNWF11_Beta
The Microchip's RNWF11 Wi-Fi™ Modules are an attach solution which can enable Wi-Fi and IoT Cloud
connectivity on any existing designs. The RNWF11 modules are designed to reduce the user application
development time by providing ASCII based AT Commands over the UART interface to expose its features and
capabilities. As the RNWF11 handles all the Wi-Fi and IoT cloud related functionality, even a simple 8-bit Host
microcontroller can have the cloud connectivity with minimal hardware requirements. The ASCII AT command
interface provides an easier evaluation of the board using any standard serial port application on a PC.
The RNWF11 Add On Board is an efficient, low-cost development platform to evaluate and demonstrate the
features and functionality of Microchip’s low-power Wi-Fi RNWF11PC Module. It can be used with a Host PC
via USB interface without the need of an additional hardware accessory. This is compliant to the mikroBUS™
Standard. The Add On Board can be plugged easily on the host board and can be controlled by Host
Microcontroller Unit (MCU) with AT commands through UART.
The RNWF11 Add On Board offers:
1. Easy-to-use platform to speed-up design concepts to revenue with the low-power Wi-Fi RNWF11PC Module:
- Host PC via USB Type-C™ interface.
- Host board supporting mikroBUS socket.
2. ATECC608B Crypto Authentication Trust Flex IC device for secure and authenticated cloud connection.
3. Pre-programmed, easy- to-use, low-cost Wi-Fi adapter.

## Features

1. Easy to learn ASCII AT commands for adding Wi-Fi and Cloud connectivity to any processor
2. Mutual authentication supported with AWS and Azure
3. Server authentication supported for test.mosquitto.org
4. Designed for RNWF11 module with integrated Trust&Go (TNG) or Trustflex (Trustflex is mounted on the RNWF11 EVB, which makes it very easy for development)
5. Ready to use RNWF11 module to connect to different cloud vendors by just changing the configuration values (single image supports connectivity with AWS / Azure / test.mosquitto.org)
6. Supports MQTT, Socket programming(TCP/ UDP), SNTP, TLS (v1.2), ICMP, IGMP, DNS, DHCP, WPA3, Loading Certificates via UART, WiFi Provisioning.
    
## Hardware Setup
### Hardware Requirements

- RNWF11 Add On board
- Access Point with Internet

## Solution block diagram
### Solution Overview

The RNWF11 firmware can connect to any of the three Clouds- AWS, Azure or test.mosquitto.org without simple AT configuration commands.

## Evaluating the Solution

Perform the following steps:

1. Connect the RNWF11 Add On board to your PC/ Host MCU.
2. Open the Terminal application (Ex.:Tera term) on the computer.
3. Connect to the "USB to UART" COM port and configure the serial settings as follows:
- Baud : 230400
- Data : 8 Bits
- Parity : None
- Stop : 1 Bit
- Flow Control : None
4. All the configurations on the device will be done using AT Cmds via the UART. The details regarding the supported AT CMDs can be found in the document ATCommandReference.pdf in the "doc" folder
5. Configure the home AP credentials using the AT Cmds
    Example:
    
        AT+WSTAC=1,"DEMO_AP"
        AT+WSTAC=2,3
        AT+WSTAC=3,"password"
        AT+WSTAC=4,255
        AT+WSTAC=12,"pool.ntp.org"
        AT+WSTAC=13,1
        AT+WSTA=1
   
6. The device connects to the Wi-Fi and the IP address is assigned, and relevant AT Cmd response is sent to UART.
Example:

        +WSTAAIP:1,"2401:4900:270A:4703:DA47:8FFF:FE68:FAA3"
        
7. Configure the device to connect to Cloud - in this case either of AWS or Azure or test.mosquitto.org
Example:

        AT+MQTTC=1,"youramazonaws.com"
        AT+MQTTC=2,8883
        AT+MQTTC=3,"yourDeviceId"
        AT+MQTTC=7,1
        AT+MQTTC=6,60
        AT+MQTTCONN=1
        
Note: One needs to register the device certificate with AWS and Azure portal in case the user wants to connect to either of these cloud vendors. More details in Cloud Setup Procedure document.

The device connects to the Cloud, and relevant AT Cmd response is sent to UART.

Below is a sample output which comes on UART when a device connects to AWS cloud. Please refer to the AT Command Reference Manual to get more details about each of the line below.

Example:

        +MQTTPROPRX:33
        +MQTTPROPRX:36
        +MQTTPROPRX:37
        +MQTTPROPRX:39
        +MQTTPROPRX:34
        +MQTTPROPRX:40
        +MQTTPROPRX:41
        +MQTTPROPRX:42
        +MQTTPROPRX:19
        +MQTTCONNACK:0,0
        +MQTTCONN:1
        
## Secure Provisioning & Transport Layer Security

The RNWF11 Add On Boards kits are shipped with the RNWF11 module variant that include an on-board Trust&Go secure element. Since Trust&Go devices are pre-provisioned, the customer does not need to programe the device certificate for each of his devices and the firmware can utilise the on-chip certificate to securely authenticate with AWS IoT Core/ Azure IoT Hub.
