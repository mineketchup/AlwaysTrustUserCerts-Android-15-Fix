# Personally modified for Android 15
## How to use
- install this module from Releases
- install [MoveCertificate](https://github.com/ys1231/MoveCertificate)
- install your user certificate from Settings>Security>Certificate of your Phone
- Reboot and check if it's working

## 502 Certificate verify failed
In case you run softwares like mitmproxy on-device but your browser shows `502 Bad Gateway Certificate verify failed: unable to get local issuer certificate` run the next command on Termux to fix it:
- `cat [PATHtoCERTIFICATEpemFILE] >> cat $(python -m certifi)`

## Why this fork
Personally the original module was not working for me: 
- certificates are mounted on APEX's /cacert directory when checked from Termux but not when checking with a Root File Explorer
- fix for the above issue was solved by using [MoveCertificate](https://github.com/ys1231/MoveCertificate)
- but now, user certificate are not available on /system/etc/security/cacert/
- so I thought modifying the script of this module just to use the part for /system/etc/security/cacert was the best thing

Below is the original text from the repo:

---

# Always Trust User Certs

This module makes all installed user certificates part of the system certificate store, so that they will automatically be used when building the trust chain. This module makes it unnecessary to add the network_security_config property to an application's manifest.

Features:

* Support for multiple users
* Support for Magisk/KernelSU/KernelSU Next
* Support for devices with and without mainline/conscrypt updates

Depending on your Android version and Google Play Security Update version, your certificates will be either stored in `/system/etc/security/cacerts` or in `/apex/com.android.conscrypt/cacerts/`. This module handles all scenarios and works on any device from Android 7 until Android 16.

More background information can be found [in this blogpost](https://blog.nviso.eu/2025/06/05/intercepting-traffic-on-android-with-mainline-and-conscrypt/).
## Usage

### Installing certificates

Install the certificate as a user certificate and restart the device.

### Removing certificates

Remove the certificate from the user store through the settings and restart the device.

## Changelog

### v1.3

* Fixed bug on A14+

### v1.2

* Added automatic update support

### v1.1

* Fixed permission issue for non-conscrypt
* Fixed removal of certs for non-conscrypt
* Renamed repo

### v1.0

* Add support for mainline/conscrypt certificates
* Add support for multiple users
* Add support for KernelSU

### v0.4.1

* Supports Android 10
* Updated Module to be compatible with latest Magisk module template (v20.4+)

### v0.3

* The module now removes all user-installed certificates from the system store before copying them over, so that user certificates that were removed will no longer be kept in the system store.

### v0.2

* Fixed directory creation bug
* Updated Module to be compatible with latest Magisk module template (v15+)

### v0.1

* Initial release
