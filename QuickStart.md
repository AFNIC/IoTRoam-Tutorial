 1. [Verify] whether the required ports are open between the different interfaces  
 2. [Check] the Gateway Set up 
 3. [Validate] that the NS receives data from the RGW 
 4. [Make sure]  that the AS receives data from the NS  
 5. Verify that you have provisioned your NetID and JoinEUI to the [DNS] 
 6. For the Certificates
    * a.) Clone/Copy the required [Files] 
    * b.) The directory structure is as [here]
    * b.) Modify [intermediate-csr.json]  to suit you
    * c.) Modify "Certificate.json" in all subdirectories to suit your "CN" and host "IP addresses"
    * d.) For roaming, You have to modify the directory name to suit your NetId. In the [example], the NetID is "000000"
 7. Install [cfssl]. A Short installation [tutorial]
 8. Following has to be done to run the [Makefile]
    * a.) Request your intermediate public and private certificate by sending mail to `"sandoche.balakrichenan@afnic.fr"` AND `"antoine.bernard@afnic.fr"`
    * b.) Copy the intermediate public and private certificate to the intermediate directory as specified in the directory structure as [here]: 
    * c.) Modify the `NetId` in the top of the `Makefile` to suit your `NetId`
    * d.) Run `make`
 9. Make sure that your `.toml`config files are correctly configured
    * a.) Sample [Network-Server-Config] file. For detailed information, [chirpstack-network-server-config] page
    * b.) Sample [Application-Server-Config] file. For detialed information, [chirpstack-application-server-config] page
10. Launch the NS and the AS 
    * a.) Initial [Configuration] of the Web interface : 
    * b.) One needs to add *Certain* [Client certificates] to the Web interface to enable encryption between AS and NS. 
11. For Roaming, in the Web interace [define] the home NetID of a device, define a variable called "home_netid" with as value for example "000001" if that is the home NetID you would like to assign.
12. Once everything  is done, send a Join-Request from your device to check the passive roaming OTAA.



[Verify]: https://github.com/AFNIC/IoTRoam-Tutorial/blob/master/Architecture.md
[Check]: https://github.com/AFNIC/IoTRoam-Tutorial/blob/master/Gateway-Setup.md#Post-Sanity-check
[Validate]: https://github.com/AFNIC/IoTRoam-Tutorial/blob/master/NetworkServer-Server-Setup.md#post-sanity-check-from-rgw-ns-setup
[Make sure]: https://github.com/AFNIC/IoTRoam-Tutorial/blob/master/ApplicationServer-Setup.md#post-sanity-check-from-rgw-ns-as-setup
[DNS]: https://github.com/AFNIC/IoTRoam-Tutorial/blob/master/DNS-Setup.md#how-to-provision-netids-and-joineuis-in-the-dns-for-otaa-and-roaming
[Files]: https://github.com/AFNIC/IoTRoam-Tutorial/tree/master/certificates
[here]: https://github.com/AFNIC/IoTRoam-Tutorial/blob/master/Certificates-Tutorial.md#directory-structure
[intermediate-csr.json]: https://github.com/AFNIC/IoTRoam-Tutorial/blob/master/certificates/config/intermediate-csr.json 
[example]: https://github.com/AFNIC/IoTRoam-Tutorial/tree/master/certificates/config/network-server/roaming/000000
[cfssl]: https://blog.cloudflare.com/introducing-cfssl/
[tutorial]: https://computingforgeeks.com/how-to-install-cloudflare-cfssl-on-linux-macos/
[Makefile]: https://github.com/AFNIC/IoTRoam-Tutorial/edit/master/certificates/Makefile
[Network-Server-Config]: https://github.com/AFNIC/IoTRoam-Tutorial/blob/master/Server-Config-Files/chirpstack-network-server.toml
[chirpstack-network-server-config]: https://www.chirpstack.io/network-server/install/config/
[Application-Server-Config]: https://github.com/AFNIC/IoTRoam-Tutorial/blob/master/Server-Config-Files/chirpstack-application-server.toml
[chirpstack-application-server-config]: https://www.chirpstack.io/application-server/install/config/
[Configuration]: https://github.com/AFNIC/IoTRoam-Tutorial/blob/master/ApplicationServer-Setup.md#web-interface-setup
[Client certificates]: https://github.com/AFNIC/IoTRoam-Tutorial/blob/master/Certificate-Provisioning-Via-Web-Interface.md
[define]: https://github.com/AFNIC/IoTRoam-Tutorial/blob/master/Passive-Roaming.md
