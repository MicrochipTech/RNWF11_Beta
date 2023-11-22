# RNWF11_Beta
Repository to enable evaluation of RNWF11

Client are often challenged by fast and easy onboarding of Wifi product to a given cloud. Microchip aims to make all these steps easy for the customer. This Solution allows easy connectivity to AWS, Azure and test.mosquitto.org with RNWF11.

## Features

1. Easy to learn ASCII AT commands for adding Wi-Fi and Cloud connectivity to any processor
2. Mutual authentication supported with AWS and Azure
3. Server authentication supported for test.mosquitto.org
4. Designed for RNWF11 module with integrated Trust&Go (TNG) or Trustflex (Trustflex is mounted on the RNWF11 EVB, which makes it very easy for development)
5. Ready to use RNWF11 module to connect to different cloud vendors by just changing the configuration values (single image supports connectivity with AWS / Azure / test.mosquitto.org)
6. Supports MQTT, Socket programming(TCP/ UDP), SNTP, TLS (v1.2), ICMP, IGMP, DNS, DHCP, WPA3, Loading Certificates via UART, WiFi Provisioning.
    
## Hardware Setup
### Hardware Requirements

    RNWF11 Add On board
    Access Point with Internet

## Solution block diagram
### Solution Overview

The Solution code is written as a FreeRTOS based MPLAB Harmony3 solution that leverages the system service-based architecture of PIC32MZ W1. The Solution can connect to any of the three Clouds- AWS, Azure or test.mosquitto.org without the need for recompiling of the image.

## Evaluating the Solution

Perform the following steps:

    Connect the RNWF11 Add On board to your PC/ Host MCU.

    Open the Terminal application (Ex.:Tera term) on the computer.

    Connect to the "USB to UART" COM port and configure the serial settings as follows:

        Baud : 230400

        Data : 8 Bits

        Parity : None

        Stop : 1 Bit

        Flow Control : None

    Note: The UART used in this case is UART2.

    All the configurations on the device will be done using AT Cmds via the UART. The details regarding the supported AT CMDs can be found in the document ATCommandReference.pdf in the "doc" folder

    Configure the home AP credentials using the AT Cmds

    Example:

     AT+WSTAC=1,"DEMO_AP"
     AT+WSTAC=2,3
     AT+WSTAC=3,"password"
     AT+WSTAC=4,255
     AT+WSTAC=12,"pool.ntp.org"
     AT+WSTAC=13,1
     AT+WSTA=1

The device connects to the Wi-Fi and the IP address is assigned, and relevant AT Cmd response is sent to UART.

Example:

+WSTALU:"42:2C:62:CC:C0:0B",11
+WSTAAIP:"192.168.159.108"
+TIME:2,3864185092

Configure the device to connect to Cloud - in this case either of AWS or Azure or test.mosquitto.org

Example:

AT+MQTTC=1,"youramazonaws.com"
AT+MQTTC=2,8883
AT+MQTTC=3,"yourDeviceId"
AT+MQTTCONN=1

Note: One needs to register the device certificate with AWS and Azure portal in case the user wants to connect to either of these cloud vendors. More details in Cloud Setup Procedure document.

The device connects to the Cloud, and relevant AT Cmd response is sent to UART.

Example:

 +MQTTCONNACK:0,0
 +MQTTCONN:1

Secure Provisioning & Transport Layer Security

The RNWF11 Add On Boards kits are shipped with the RNWF11 module variant that include an on-board Trust&Go secure element. Since Trust&Go devices are pre-provisioned, the customer does not need to programe the device certificate for each of his devices and the firmware can utilise the on-chip certificate to securely authenticate with AWS IoT Core/ Azure IoT Hub.
