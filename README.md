# MBED TLS Example program on NUCLEO L476RG + ESP8266

This is basically a copy of the mbed-tls example adopted on a Nucleo L476RG development board with an attached ESP8266 used for Wifi connections. I will be using this as a springboard for my mbed projects with Wifi and mbed tls support.

## Description

This is an mbed project to test mbed tls (Transport Layer Security) for an mbed running on a Nucleo board (NUCLEO_L476RG).
It connect to a secure (https) server and verifies the server signature (just print it out on screen). Downloads the page and displays it on screen.

The Nucleo L476RG board is using the ESP8266 for wifi connection. I have connected A0 (TX) and A1 (RX) on Nucleo L476RG to connect to ESP8266
TX/RX (Rx -> Tx/ Tx -> Rx). You may be able to change this via mbed_app.json to suit your configuration.

## Quick Steps to compile
This project is built using mbed-cli and not the online compiler. Please refer to mbed-cli on how to install and use it on your system

**>mbed import https://github.com/vpcola/nucleoesp.git test**
```
[mbed] Importing program "test" from "https://github.com/vpcola/nucleoesp.git" at latest revision in the current branch
[mbed] Adding library "easy-connect.git" from "https://github.com/ARMmbed/easy-connect" at rev #559d00bf1580
[mbed] Adding library "easy-connect.git\atmel-rf-driver" from "https://github.com/ARMmbed/atmel-rf-driver" at rev #ca9782e68f5f
[mbed] Adding library "easy-connect.git\esp8266-driver" from "https://github.com/ARMmbed/esp8266-driver" at rev #264468722a97
[mbed] Adding library "easy-connect.git\mcr20a-rf-driver" from "https://github.com/ARMmbed/mcr20a-rf-driver" at rev #93661a696735
[mbed] Adding library "easy-connect.git\stm-spirit1-rf-driver" from "https://github.com/ARMmbed/stm-spirit1-rf-driver" at rev #ce9e2f81f95f
[mbed] Adding library "easy-connect.git\wifi-ism43362" from "https://github.com/ARMmbed/wifi-ism43362" at rev #d47a8c2fba0e
[mbed] Adding library "easy-connect.git\wifi-x-nucleo-idw01m1" from "https://github.com/ARMmbed/wifi-x-nucleo-idw01m1" at rev #257d0878561b
[mbed] Adding library "easy-connect.git\wizfi310-driver" from "https://github.com/ARMmbed/wizfi310-driver" at rev #e0f7b9355e7e
[mbed] Adding library "mbed-os" from "https://github.com/ARMmbed/mbed-os" at rev #569159b784f7
```
**>cd test**
**>mbed target NUCLEO_L476RG**
```
[mbed] NUCLEO_L476RG now set as default target in program "test"
```
**>mbed toolchain GCC_ARM**
```
[mbed] GCC_ARM now set as default toolchain in program "test"
```
**>mbed compile**
```
Building project test (NUCLEO_L476RG, GCC_ARM)
Scan: .
Scan: mbed
Scan: env
Scan: FEATURE_COMMON_PAL
Scan: FEATURE_NANOSTACK
Compile [  0.2%]: easy-connect.cpp
Compile [  0.4%]: ESP8266Interface.cpp
Compile [  0.5%]: NanostackRfPhyAtmel.cpp
[Warning] NanostackRfPhyAtmel.cpp@1100,18: variable 'last_is' set but not used [-Wunused-but-set-variable]
[Warning] NanostackRfPhyAtmel.cpp@1100,27: variable 'last_ts' set but not used [-Wunused-but-set-variable]
[Warning] NanostackRfPhyAtmel.cpp@1102,11: unused variable 'orig_xah_ctrl_1' [-Wunused-variable]
[Warning] NanostackRfPhyAtmel.cpp@1106,11: unused variable 'orig_flags' [-Wunused-variable]
[Warning] NanostackRfPhyAtmel.cpp@1377,13: 'void rf_ack_wait_timer_stop()' defined but not used [-Wunused-function]
Compile [  0.7%]: at24mac.cpp
...
...
Compile [ 99.6%]: us_ticker_16b.c
Compile [ 99.8%]: us_ticker_32b.c
Compile [100.0%]: test_env.cpp
Link: test
Elf2Bin: test
Text 237KB Data 2.79KB BSS 9.11KB ROM 240KB RAM 11.9KB
Image: .\BUILD\NUCLEO_L476RG\GCC_ARM\test.bin

```
After which, you can then transfer the *.bin file in BUILD\NUCLEO_L476RG\GCC_ARM\test.bin to your target board\drive.

## Target board (NUCLEO_L476RG) running ...

```
Starting mbed-os-example-tls/tls-client
Using Mbed OS 5.7.5
[EasyConnect] IPv4 mode
Connecting with os.mbed.com
Starting the TLS handshake...
TLS connection to os.mbed.com established
Server certificate:
    cert. version     : 3
    serial number     : 65:7B:6D:8D:15:A5:B6:86:87:6B:5E:BC
    issuer name       : C=BE, O=GlobalSign nv-sa, CN=GlobalSign Organization Val                       idation CA - SHA256 - G2
    subject name      : C=GB, ST=Cambridgeshire, L=Cambridge, O=ARM Ltd, CN=*.mb                       ed.com
    issued  on        : 2017-04-03 13:54:02
    expires on        : 2018-05-06 10:31:02
    signed using      : RSA with SHA-256
    RSA key size      : 2048 bits
    basic constraints : CA=false
    subject alt name  : *.mbed.com, mbed.org, *.mbed.org, mbed.com
    key usage         : Digital Signature, Key Encipherment
    ext key usage     : TLS Web Server Authentication, TLS Web Client Authentica                       tion
Certificate verification passed

HTTPS: Received 365 chars from server
HTTPS: Received 200 OK status ... [OK]
HTTPS: Received 'Hello world!' status ... [OK]
HTTPS: Received message:

HTTP/1.1 200 OK
Server: nginx/1.11.12
Date: Mon, 19 Feb 2018 15:40:31 GMT
Content-Type: text/plain
Content-Length: 14
Connection: keep-alive
Last-Modified: Fri, 27 Jul 2012 13:30:34 GMT
Accept-Ranges: bytes
Cache-Control: max-age=36000
Expires: Tue, 20 Feb 2018 01:40:16 GMT
Strict-Transport-Security: max-age=31536000; includeSubdomains

Hello world!

```

## Requirements
* Nucleo L476RG
* ESP8266 module flashed with latest firmware.
