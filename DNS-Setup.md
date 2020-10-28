This page covers the following: 

 * [Why do we need the DNS Infrastructure?] 
 * [How to Provision NetIDs and JoinEUIs in the DNS for OTAA and Roaming?]


## Why the DNS infrastructure is required in the LoRaWAN set up?

As per the LoRaWAN Backend specifications, the DNS infrastructure is used for the following operations:

1.	OTAA: By the NS to get the IP address of the Join Server
2.  Roaming: By the vNS (Visited NS) to find the hNS (Home NS)
3.  OTAA: Associate a batch of devices to one specific Join Server using a DNS look-up, combining DevEUI and JoinEUI

Two types of identifiers are provisioned in the DNS - 
1. NetIDS for Roaming and 
2. JoinEUI for OTAA 

As per the backend specification, the LoRa Alliance DNS tree is as shown in the below figure:

<p align="center">
  <img width="760" height="400" src="https://github.com/afnic/IoTRoam-Tutorial/blob/master/Images/Fig11.png?raw=true">
</p>


## How to Provision NetIDs and JoinEUIs in the DNS for OTAA and Roaming?

As of now, the LoRa DNS service is not operational. Hence, for the Academic LoRaWAN roaming purposes we have a separate zone called ```iotreg.net``` where the NetIDs and JoinEUIs could be provisioned as shown in the figure below:

<p align="center">
  <img width="760" height="400" src="https://github.com/afnic/IoTRoam-Tutorial/blob/master/Images/Fig12.png?raw=true">
</p>

To provision the information in the DNS (Currently only the JoinEUI info), Send your JoinEUI information (i.e. the Join EUI and the corresponding JS domain name or IP address) to  sandoche.balakrichenan@afnic.fr AND antoine.bernard@afnic.fr. 

If you are confused regarding JoinEUI and NetID:
  a.) There is a [discussion]
  b.) Make sure that your test NetID or JoinEUI is not yet provisioned in the roaming platform
 
## Verify that your JoinEUI and NetID is publicly accessible

Once the JoinEUI information is updated to the DNS, one can verify whether the information is updated properly by reversing the JoinEUI, delimiting by ‘.’ and adding the suffix “joineuis.iotreg.net” and testing using the ```dig``` utility as shown inthe figure:

<p align="center">
  <img width="760" height="75" src="https://github.com/afnic/IoTRoam-Tutorial/blob/master/Images/Fig13.png?raw=true">
</p>



## Pointer Section

Once verified that your NetID and JoinEUI provisioned in the Internet are publicly accessible, Next section to follow : [OTAA-Setup  Using DNS]


 * In any case, If you want to go back to the [Readme Page]
 * In any case, If you want to go back to the [Architecture page]
 * In any case, If you want to go back to the [Setting up the End-Device]
 * In any case, If you want to go back to the [Setting up the GW]
 * In any case, If you want to go back to the [NS Setup]
 * In any case, If you want to go back to the [AS Setup]

[Why do we need the DNS Infrastructure?]: #why-the-dns-infrastructure-is-required-in-the-lorawan-set-up
[How to Provision NetIDs and JoinEUIs in the DNS for OTAA and Roaming?]: #how-to-provision-netids-and-joineuis-in-the-dns-for-otaa-and-roaming
[NS Setup]: https://github.com/afnic/IoTRoam-Tutorial/blob/master/NetworkServer-Server-Setup.md
[AS_Setup]: https://github.com/afnic/IoTRoam-Tutorial/blob/master/ApplicationServer-Setup.md
[Setting up the GW]: https://github.com/afnic/IoTRoam-Tutorial/blob/master/Gateway-Setup.md
[Architecture page]: https://github.com/afnic/IoTRoam-Tutorial/blob/master/Architecture.md
[Readme Page]: https://github.com/afnic/IoTRoam-Tutorial
[Setting up the End-Device]: https://github.com/afnic/IoTRoam-Tutorial/blob/master/End-Device.md
[NS Setup]: https://github.com/afnic/IoTRoam-Tutorial/blob/master/NetworkServer-Server-Setup.md
[AS Setup]: https://github.com/afnic/IoTRoam-Tutorial/blob/master/ApplicationServer-Setup.md
[OTAA-Setup  Using DNS]: https://github.com/afnic/IoTRoam-Tutorial/blob/master/OTAA-Using-DNS.md
[discussion]: https://github.com/AFNIC/IoTRoam-Tutorial/issues/2

