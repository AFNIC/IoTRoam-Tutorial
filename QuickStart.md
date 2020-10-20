 1. Verify whether the required ports are open between the different interfaces : https://github.com/AFNIC/IoTRoam-Tutorial/blob/master/Architecture.md
 2. Check the Gateway Set up : https://github.com/AFNIC/IoTRoam-Tutorial/blob/master/Gateway-Setup.md#Post-Sanity-check
 3. Check the whether the NS receives data from the RGW : https://github.com/AFNIC/IoTRoam-Tutorial/blob/master/NetworkServer-Server-Setup.md#post-sanity-check-from-rgw-ns-setup
 4. Verify whether the AS receives data from the NS : https://github.com/AFNIC/IoTRoam-Tutorial/blob/master/ApplicationServer-Setup.md#post-sanity-check-from-rgw-ns-as-setup
 5. Verify that you have provisioned your NetID and JoinEUI to the DNS : https://github.com/AFNIC/IoTRoam-Tutorial/blob/master/DNS-Setup.md#how-to-provision-netids-and-joineuis-in-the-dns-for-otaa-and-roaming
 6. For the Certificates
    a.) Clone/Copy the required Files : https://github.com/AFNIC/IoTRoam-Tutorial/tree/master/certificates
    b.) The directory structure is as here : https://github.com/AFNIC/IoTRoam-Tutorial/blob/master/Certificates-Tutorial.md#directory-structure
    b.) Modify intermediate-csr.json : https://github.com/AFNIC/IoTRoam-Tutorial/blob/master/config/intermediate-csr.json to suit you
    c.) Modify "Certificate.json" in all subdirectories to suit your "CN" and host "IP addresses"
    d.) For roaming, You have to modify the directory name to suit your NetId. In the example (https://github.com/AFNIC/IoTRoam-Tutorial/tree/master/config/network-server/roaming/000000), the NetID is "000000"
 7. Install cfssl (https://blog.cloudflare.com/introducing-cfssl/). Some cfssl  installation tutorial : https://computingforgeeks.com/how-to-install-cloudflare-cfssl-on-linux-macos/
 8. Following has to done to run the Makefile : https://github.com/AFNIC/IoTRoam-Tutorial/edit/master/certificates/Makefile
    a.) Request your intermediate public and private certificate by sending mail to "sandoche.balakrichenan@afnic.fr" AND "antoine.bernard@afnic.fr"
    b.) Copy the intermediate public and private certificate to the intermediate directory as specified in the directory structure : https://github.com/AFNIC/IoTRoam-Tutorial/blob/master/Certificates-Tutorial.md#directory-structure
    c.) Modify the `NetId` in the top of the `Makefile` to suit your `NetId`
    d.) Run `make`
 9. Make sure that your `.toml`config files are correctly configured
    a.) Sample Network-Server-Config files https://github.com/AFNIC/IoTRoam-Tutorial/blob/master/Server-Config-Files/chirpstack-network-server.toml. For more information : https://www.chirpstack.io/network-server/install/config/
    b.) Sample Application-Server-Config files https://github.com/AFNIC/IoTRoam-Tutorial/blob/master/Server-Config-Files/chirpstack-application-server.toml. For more information : https://www.chirpstack.io/application-server/install/config/
10. Launch the NS and the AS 
    a.) Initial Configuration of the Web interface : https://github.com/AFNIC/IoTRoam-Tutorial/blob/master/ApplicationServer-Setup.md#web-interface-setup
    b.) One needs to add *Certain* Client certificates to the Web interface. 