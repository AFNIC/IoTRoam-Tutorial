This page provides an introduction to the Join Server (JS), JoinEUI and configuring the NS to enable DNS resolution. The DNS resolution is required when the ED is not known to the NS and it needs the DNS resolution to identify the JS for the ED and complete the OTAA.

 * [JS Brief Intro]
 * [Configuring NS to access the JS using DNS]
 * [Provisioning in the DNS]
 * [OTAA Verification using DNS]

 ## JS Brief Intro
 
JS is used for authenticating the end-devices, is also identified by a 64-bit globally unique identifier termed as AppEUI/JoinEUI. The JS could be a separate server or same as the AS. In our set up the JS and AS functionalities runs in the same physical machine as shown in the figure below:

<p align="center">
  <img width="760" height="300" src="https://github.com/afnic/IoTRoam-Tutorial/blob/master/Images/Fig14.png?raw=true">
</p>
 
 
## Configuring NS to access the JS using DNS

When the ED sends a Join Request (JR) as per the [LoRaWAN Backend Specifications], the RGW will forward the JR to the NS. If the ED is not known to the NS, then it generates a DNS query to securely communicate with the JS. 

In order to enable DNS resolution, the configuration file is located in the NS folder in ```/etc```. It is a ```toml``` file:

```sh
$ /etc/chirpstack-network-server/chirpstack-network-server.toml
```

Jump to the ```[join_server]``` section which is used to find the Join Server relevant to a given JoinEUI. The default configuration always uses the fallback method of using a default Join Server to resolve it (this Join Server being the Application Server). We will also setup the ```[join_server.default]``` parameter to contact our Application Server but we wish to enable the JoinEUI resolution. 

The configuration file already specifies the ```resolve_domain_suffix``` corresponding to the LoRa Alliance service for JoinEUI resolution, so we just have to change the resolve_join_eui Boolean to true to set things right:


```sh
[join_server]
.
.
resolve_join_eui=true
.
.
resolve_domain_suffix=”.joineui.iotreg.net”
```
The above configuration will enable the NS to generate a DNS query and concatenate the JoinEUI with a sub domain as specified in the LoRaWAN Backend Specifications.    
   
In addition, if your JS is not hosted on the same server as your NS, you will also need to change the ```[join_server.default]``` parameter with the IP address of your JS

```sh
[join_server]
.
.
   [join_server.default]
   .
   .  
   server=http://192.168.2.12:443  # Your JS-IP and port 443 
```
 
## Configuring the ED to access the JS using DNS

In the [Web Interfaces Setup], it is shown how config (like the AppKey) is added to the ED for Multitech Mdot? We need to add the JoinEUI/AppEUI also. The issue with the Chirpstack, unlike Things Network LoRaWAN backend, there is no unique AppEUI or JoinEUI generated. Hence we add a unique AppEUI/JoinEUI of the format as below: 
```sh
       00005E100000002F
```

This is done by adding to the ED for mDot as follows

```sh
         AT+NJM=1                  # To enable join OTAA mode
         AT+NI=0, 00005E100000002F # Set your AppEUI/JoinEUI
```

Make sure that you save the setting and also test whether your new settings has been updated by using following commands:

```sh
                 AT&W            ## Save Configuration to flash memory
                 AT&V            ##  Display current settings and status
```

## Provisioning in the DNS

Afnic manages the DNS provisioning and the more infiormation is explained in the section: [How to Provision in the DNS?].

As per the [LoRaWAN Backend Specifications], each of the AppEUI/JoinEUI nibble are encoded in reverse order and periods are added between each hexadecimal digit. Finally the domain name “JOINEUIS.lorawan.net” is concatenated as suffix to the encoded hexadecimal conversion of the JoinEUI. In our set up instead of “JOINEUIS.lorawan.net”, we are using “JOINEUI.iotreg.net”. An example on how it is provisioned in the DNS is as follows:


```sh
     f.2.0.0.0.0.0.0.0.1.e.5.0.0.0.0.joineui.iotreg.net. IN A 	192.168.2.3  ## Your JoinServer IP address
```

## Post Sanity Check from RGW->NS->DNS->AS Setup

The objective in this section is to verify the communication between the RGW->NS (2), NS->DNS (3), DNS->NS (4) and NS->AS (5) as shown in the figure:

<p align="center">
  <img width="800" height="400" src="https://github.com/afnic/IoTRoam-Tutorial/blob/master/Images/Fig24.png?raw=true">
</p>

### Verify whether the NS receives data from the RGW

[LoRaWAN Backend Specifications]: https://lora-alliance.org/resource-hub/lorawanr-back-end-interfaces-v10
[Configuring NS to access the JS using DNS]: #configuring-ns-to-access-the-js-using-dns
[JS Brief Intro]: #js-brief-intro
[Web Interfaces Setup]: https://github.com/afnic/IoTRoam-Tutorial/blob/master/ApplicationServer-Setup.md#web-interface-setup
[Provisioning in the DNS]: #provisioning-in-the-dns
[How to Provision in the DNS?]: https://github.com/afnic/IoTRoam-Tutorial/blob/master/DNS-Setup.md#how-to-provision-netids-and-joineuis-in-the-dns-for-otaa-and-roaming
