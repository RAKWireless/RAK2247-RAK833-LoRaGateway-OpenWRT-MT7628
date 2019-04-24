# Welcome to the WisLora wiki!
The WisLora is WisAp(Mt7628 + OpenWRT) and Lora gateway, here to use RAK833. It is based on the latest SX1301 driver lora_gateway v5.0.1 and semtech packet_forwarder v4.0.1. We've tested it with TTN.

# RAK833 USB interface usage

## Compile SDK

Compile dependency with ubuntu 14.04

	sudo apt-get install build-essential subversion git-core libncurses5-dev zlib1g-dev gawk flex quilt libssl-dev xsltproc libxml-parser-perl mercurial bzr ecj cvs unzip

### Step 1: Clone SDK
Open terminal, and type the following:<br>

    cd Desktop
    git clone https://github.com/RAKWireless/RAK833-LoRaGateway-OpenWRT-MT7628.git RAK833-LoRaGateway-OpenWRT-MT7628-USB


### Step 2: to set compile environment
Before you run make, you need to set compile environment first with envsetup.sh.

    cd ~/Desktop/RAK833-LoRaGateway-OpenWRT-MT7628-USB
    sudo ./build/envsetup.sh

### Step 3: Run Make to compile

    sudo make

Finally compiled generated files firmware in the folder out/target/bin


## Burn firmware to the board

    cp ~/Desktop/RAK833-LoRaGateway-OpenWRT-MT7628-USB/out/target/bin/firmware /windows/

[How to burn firmware to Board](https://github.com/RAKWireless/wiscore/wiki/Burn-firmware-to-MT762x-Board)<br>


## To Use LoraGW

1. Register an account in [The Things Network Control](https://console.thethingsnetwork.org), then login and register gateway

* Click "GATEWAYS"
<div align=center> <img src="https://github.com/RAKWireless/wiscore/blob/master/img/ThingsC_home.png" /> </div>

* Click "register gateway"
<div align=center> <img src="https://github.com/RAKWireless/wiscore/blob/master/img/ThingsC_reg1.png" /> </div>

* Fill in, "Gateway EUI" is unique and must consist of exactly 8 bytes hexadecimal, and choose "Frequency Plan", here use 868MHz
<div align=center> <img src="https://github.com/RAKWireless/wiscore/blob/master/img/ThingsC_reg2.png" /> </div>

* Click "Register Gateway"
<div align=center> <img src="https://github.com/RAKWireless/wiscore/blob/master/img/ThingsC_reg3.png" /> </div>

* Finally you will see the gateway overview, and Status is not connected
<div align=center> <img src="https://github.com/RAKWireless/wiscore/blob/master/img/ThingsC_reg4.png" /> </div>

2. Power on, then [setup wifi](https://github.com/RAKWireless/wiscore/wiki/Setup-Wireless) or connect to your router with WisAp WAN port directly.

3. Connect RAK833 to WisAp usb port

4. Check the connection of RAK833 and WisAp, excute:

	/usr/bin/lora/test_loragw_reg

It will display:
<div align=center> <img src="https://github.com/RAKWireless/wiscore/blob/master/img/RAK831_WisAp_Spi.png" /> </div>


5. Check the ID and Service

check the gateway ID(Gateway EUI) and server address ,make sure they are consistent with [The Things Network Control](https://console.thethingsnetwork.org),

	vi /usr/bin/packet_forwarder/local_conf.json

<div align=center> <img src="https://github.com/RAKWireless/wiscore/blob/master/img/wislora_global.png" /> </div>
	
6. Start Lora Gateway

	root@OpenWrt:/usr/bin/packet_forwarder#  ./lora_pkt_fwd
	
Finally you can see the Status is connected in the gateway overview, then the gateway will be started and you can use it.
BTY. this project also tested with [loraserver](https://www.loraserver.io/).
<div align=center> <img src="https://github.com/RAKWireless/wiscore/blob/master/img/ThingsC_con.png" /> </div>


# RAK833 SPI interface usage
the RAK833 mini-PCIe module also support spi connection, here list the procedure tested on EVK-RAK833 board.


## OverView
EVK-RAK833:
<div align=center> <img src="https://github.com/RAKWireless/WisCore/blob/master/img/EVK-RAK833.png" width = "600" /> </div>

RAK833 module:

<div align=center> <img src="https://github.com/RAKWireless/WisCore/blob/master/img/rak833-pcie.png" width = "600"/> </div>
Here the RAK833 is Lora Gateway


## Compile SDK

Compile dependency with ubuntu 16.04

	sudo apt-get install build-essential subversion git-core libncurses5-dev zlib1g-dev gawk flex quilt libssl-dev xsltproc libxml-parser-perl mercurial bzr ecj cvs unzip

### Step 1: Clone SDK
Open terminal, and type the following:<br>

    cd Desktop
    git clone https://github.com/RAKWireless/RAK831-LoRaGateway-OpenWRT-MT7628.git  RAK833-LoRaGateway-OpenWRT-MT7628-SPI


### Step 2: to set compile environment
Before you run make, you need to set compile environment first with envsetup.sh.

    cd RAK833-LoRaGateway-OpenWRT-MT7628-SPI
    ./build/envsetup.sh

### Step 3: Run Make to compile

	make

Finally compiled generated files firmware in the folder out/target/bin


## Burn firmware to the board

[How to burn firmware to Board](https://github.com/RAKWireless/wiscore/wiki/Burn-firmware-to-MT762x-Board)<br>


## To Use LoraGW

1.connect jumper caps of the EVK board: URXD1/USBTX ,UTXD1/USBRX,GND/3V3/RESET/PPS/CSN/MOSI/MISO/SCK/M1 

<div align=center> <img src="https://github.com/RAKWireless/WisCore/blob/master/img/EVK-RAK833-SPI.png" width = "600" /> </div>


2.Plug RAK833 to EVK-RAK833 mini-PCIe slot.

3.Reset RAK833 module.

    cd /usr/bin
    ./reset_lgw.sh start 11

4.Check the connection of RAK833 and EVK, excute:    

    cd /usr/bin/lora
    ./test_loragw_reg

It will display:
<div align=center> <img src="https://github.com/RAKWireless/wiscore/blob/master/img/RAK831_WisAp_Spi.png" /> </div>

5.Check the ID and Service
check the gateway ID(Gateway EUI) and server address.

6.Start Lora Gateway

power on the Gateway and the packet_forwarder will auto start. check the log file at /usr/bin/packet_forwarder/log

Finally you can see the Status is connected in the gateway overview, then the gateway will be started and you can use it.
