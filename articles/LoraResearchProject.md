# Lora Research Project


[LoRa Basics™ Station](https://github.com/lorabasics/basicstation/blob/master/README.md)
[LoRa Basics™ Station documentation](https://lora-developers.semtech.com/build/software/lora-basics/lora-basics-for-gateways/)
[WM1302 Install for Raspberry Pi](https://github.com/seeed-lora/WM1302-doc)
[WM1303 LoRaWAN Gateway Module(SPI) - US915](https://electric.garden/seeed-z4t/manuals/WM1303-A-Users-Manual-Seeed-z4t-wm1303-a-ex-1-5.pdf)
[WM1303a LoraWAN Gateway Module](https://electric.garden/seeed-z4t/wm1303-lorawan-gateway-module-spi-us915-wm1303-a)

# Sence M1
## Install Raspbian-lite 

Download lastest Raspberry Pi OS image:

```
wget https://downloads.raspberrypi.org/raspios_lite_arm64/images/raspios_lite_arm64-2023-05-03/2023-05-03-raspios-bullseye-arm64-lite.img.xz
```

Raspberry Pi OS Lite 64-bit is recommended. Using Balena Etcher, flash Raspberry Pi OS image to SD card.


## Post Boot Configuration


`sudo raspi-config`

1. Select Interface Options
1. Select SSH, then select Yes to enable it
3. Select SPI, then select Yes to enable it
4. Select I2C, then select Yes to enable it
5. Select Serial Port, then select No for "Would you like a login shell..." and select Yes for "Would you like the serial port hardware..."
6. Select Advanced Options
7. Select "Network Interface Names" then select Yes to enable it
8. Select Localisation Options 
9. Select "Locale" then select value for your country
    

After this, please reboot Raspberry Pi to make sure these settings work.

## Get and compile SX1302 source code

Install git and download sx1302_hal(library and programs for SX1302 LoRa Gateway) from github:

```
sudo apt update

sudo apt install -y git
cd ~
git clone https://github.com/Lora-net/sx1302_hal
```

Move to sx1302_hal folder and compile everything:

```
cd ~/sx1302_hal
make
```

## Run the packetforwader


Ensure that the follow symbols in the `tools/reset_lgw.sh` script have the following values:

```
SX1302_RESET_PIN=17     # SX1302 reset
SX1261_RESET_PIN=5      # SX1261 reset (LBT / Spectral Scan)
```
Next copy to the packetforwarder:
```
cp tools/reset_lgw.sh packet_forwarder/
cd packet_forwarder
```
Run the packetforwader with the parameters for your locale.

```
# for WM1302 LoRaWAN Gateway Module (SPI) - US915
./lora_pkt_fwd -c global_conf.json.sx1250.US915
```

## Connect to Server



## SenseCAP M1 Hardware 
### General Information [](#general)
-----------------------------------
**SenseCAP M1** is a high-performing, ready-to-use **LoRaWAN indoor gateway** connected to the **Helium LongFiTM Network**.

It is based on Raspberry Pi 4 and embedded with a WM1302/WM1303 (Semtech SX1302/SX1303) LoRa concentrator. It provides built-in BLE, which helps you set up the device in a few simple steps and supports connecting to the internet via Wi-Fi or Ethernet.

![SenseCAP M1](https://1345559002-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F7YbcCgLCjFwfmsboPLCT%2Fuploads%2FcX030Sn3u72Kuv3a24tu%2Fsensecapm1.png?alt=media&token=9a2394ca-487e-452c-9396-4d445cfd471a)

### Features[](#features)
-------------------------

![](https://1345559002-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F7YbcCgLCjFwfmsboPLCT%2Fuploads%2FsfH97g3sgi21UtG0FIdI%2Ffeatures-final7.9-01-scaled.jpg?alt=media&token=1972a104-5552-44e5-acbe-460ed3bacb65)

#### SenseCAP M1 Features
-----------------------------------
*   **Handy Setup to Helium Network:** Ready to go within simple steps.
*   **Powered by Mature Hardware Solutions:** Raspberry Pi 4(2G/4G/8G RAM, 64G storage) and WM1302/WM1303 (Semtech SX1302/SX1303) baseband LoRa chip.
*   **Secure and Reliable:** Built-in ECC608 crypto chip, high-security authentication, and reliable connectivity.
*   **Automatic Online Upgrades:** Automatic OTA upgrades, without manual operation.
*   **Remote Diagnosis:** Built-in remote diagnostics mechanism, efficient online support.
*   **64GB Large Storage:** 64GB MicroSD card large storage, extending the lifetime of the gateway, fulfilling the memory requirement of potential upgrade.
*   **Efficient Cooling Solution:** Aluminum enclosure with a heatsink and cooling fan inside, ensuring long-term and stable operation.
*   **Multiple Accessories:** Fiberglass antenna, slider pad for sliding rod installation, and upcoming outdoor enclosure, etc.
*   **FCC and CE Certificated:** Available for personal and commercial use.
    

### Package Contents[](#package-content)
-----------------------------------
SenseCAP M1 LoRaWAN Indoor Gateway (EU868/US915) \*1

*   Power Adapter (EU/US)\*1
*   Antenna (EU868/US915) \*1
*   64GB MicroSD Card \*1
*   Quick Start Guide _\*1_
    

![Package Contents](https://1345559002-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F7YbcCgLCjFwfmsboPLCT%2Fuploads%2FfrVxoljLaKThRLaTVVYQ%2Fpackage-contents.png?alt=media&token=d2bf1676-3ce9-4afe-b8f7-3ba874583dc3)

### General Overview[](#general-overview)

#### SenseCAP M1 External Overview
-----------------------------------
![](https://1345559002-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F7YbcCgLCjFwfmsboPLCT%2Fuploads%2FvQMciRl5LMV1RVLqdbIS%2Foverview-1.png?alt=media&token=53baab44-fcb1-4cbd-95c1-eed78c25290a)

#### SenseCAP M1 Internal Overview

![](https://1345559002-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F7YbcCgLCjFwfmsboPLCT%2Fuploads%2FdiYpBh7j0I6J0a0qDnQI%2Foverview-2.png?alt=media&token=80f6e55b-bd82-402e-bb02-7780091d6e44)

### SenseCAP M1 Breakdown
-----------------------------------
![](https://1345559002-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F7YbcCgLCjFwfmsboPLCT%2Fuploads%2FpO0KDAYAUARkrDD1Cu6V%2Foverview-3.png?alt=media&token=69cd34f9-dd39-4302-98cc-cd7976b0cf6f)

#### Interfaces [](#interface)
-----------------------------------
![SenseCAP M1 Interface](https://1345559002-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F7YbcCgLCjFwfmsboPLCT%2Fuploads%2FQiHq0m9BAdRBiYLX7t1Y%2Finterface-1.png?alt=media&token=29d24d8b-b7ce-41b6-a01b-681c9c8282af)



## Dimensions[](#dimensions)
-----------------------------------
![](https://1345559002-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F7YbcCgLCjFwfmsboPLCT%2Fuploads%2F2f3D8f9PDYpHJWfc9lXb%2Fdimensions-1.png?alt=media&token=751f4999-ae98-4441-9051-be69975deaa8)

### SenseCAP M1 Dimensions

*   **Device Size** (/pcs): 154\*100\*44 mm
*   **Device Weight** (/pcs): 370g
*   **Package Size** (/pcs): 274\*175\*60 mm
*   **Package Weight** (/pcs): 675g
    
## Block Diagram[](#block-diagram)
-----------------------------------

![SenseCAP M1 Block Diagram](https://1345559002-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F7YbcCgLCjFwfmsboPLCT%2Fuploads%2FqLPjzD3fIFdWYbsVUjij%2Fblock-diagram.png?alt=media&token=d134b738-4721-47d2-8440-8c2d07360d6f)



### System Structure[](#system-structure-1)
-------------------------------------------

![SenseCAP M1 System Structure](https://1345559002-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F7YbcCgLCjFwfmsboPLCT%2Fuploads%2FIaZQwO7eZNSIgDmdgVCM%2Fsystem-structure.png?alt=media&token=7b9d23ba-39d4-4505-acad-592bace180fb)



### LED Status[](#led-status)
-----------------------------

![SenseCAP M1 LED Status](https://1345559002-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F7YbcCgLCjFwfmsboPLCT%2Fuploads%2FsKeJysO5yqWhtIWxVx2H%2FLED-status.png?alt=media&token=885692fc-34a0-4aef-85f9-ef306816edf7)



### Unit Information[](#unit-information)


-----------------------------------------

There are two sticker labels on the bottom of the SenseCAP M1.

![SenseCAP M1 Unit Information / Stickers / Labels](https://1345559002-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F7YbcCgLCjFwfmsboPLCT%2Fuploads%2FgB7LHeAgrAsB0SMawffw%2Funit-info.png?alt=media&token=39abf2eb-6798-48d4-b64d-273516145527)

These two labels on the bottom indicate important information of the unit including:

*   Model
*   S/N
*   WiFi MAC
*   ETH MAC
*   CPU ID
    
