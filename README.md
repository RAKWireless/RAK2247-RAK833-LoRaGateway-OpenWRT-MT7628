# Welcome to the WisLora wiki!
The WisLora is WisAp(Mt7628 + OpenWRT) and Lora gateway, here to use RAK833. It is based on the latest SX1301 driver lora_gateway v5.0.1 and semtech packet_forwarder v4.0.1. We've tested it with TTN.

## Compile SDK

Compile dependency with ubuntu 14.04

	sudo apt-get install build-essential subversion git-core libncurses5-dev zlib1g-dev gawk flex quilt libssl-dev xsltproc libxml-parser-perl mercurial bzr ecj cvs unzip

### Step 1: Clone SDK
Open terminal, and type the following:<br>

    cd Desktop
    git clone https://github.com/RAKWireless/RAK833-LoRaGateway-OpenWRT-MT7628.git


### Step 2: to set compile environment
Before you run make, you need to set compile environment first with envsetup.sh.

    cd ~/Desktop/RAK833-LoRaGateway-OpenWRT-MT7628
    ./build/envsetup.sh

### Step 3: Run Make to compile

	make

Finally compiled generated files firmware in the folder out/target/bin


## Burn firmware to the board

    cp ~/Desktop/RAK833-LoRaGateway-OpenWRT-MT7628/out/target/bin/firmware /windows/

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

2. Connect RAK833 to WisAp

3. Power on, then [setup wifi](https://github.com/RAKWireless/wiscore/wiki/Setup-Wireless)

4. Check the connection of RAK833 and WisAp, excute:

	/usr/bin/lora/test_loragw_reg

It will display:
<div align=center> <img src="https://github.com/RAKWireless/wiscore/blob/master/img/RAK831_WisAp_Spi.png" /> </div>


5. Check the ID and Service

check the gateway ID(Gateway EUI) and server address ,make sure they are consistent with [The Things Network Control](https://console.thethingsnetwork.org),

	vi /usr/bin/packet_forwarder/local_conf.json

<div align=center> <img src="https://github.com/RAKWireless/wiscore/blob/master/img/wislora_global.png" /> </div>
	
6. Start Lora Gateway

power on the Gateway and the packet_forwarder will auto start. check the log file at /usr/bin/packet_forwarder/log
	

Finally you can see the Status is connected in the gateway overview, then the gateway will be started and you can use it.
<div align=center> <img src="https://github.com/RAKWireless/wiscore/blob/master/img/ThingsC_con.png" /> </div>
