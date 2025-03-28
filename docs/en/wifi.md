Connecting to droid via Wi-Fi
===

> **Note** The following applies to [image version](image.md) **0.20** and up.

[RPi image](image.md) provides a pre-configured Wi-Fi access point with SSID `droid-xxxx`, where `xxxx` are four random numbers that are assigned when your Raspberry Pi is run for the first time.

Connect to this Wi-Fi using the password `droidwifi`.

<div class="image-group">
    <img src="../assets/wifi-ssid.png" width=300 class="zoom">
    <img src="../assets/wifi-pass.png" width=300 class="zoom">
</div>

To edit Wi-Fi settings, or to obtain more detailed information about the network device on Raspberry Pi, read this [article](network.md).

## Web interface

After connecting to droid Wi-Fi, open http://192.168.11.1 in you web browser. It contains all the basic web tools of droid: viewing image topics, web terminal (Butterfly), and the full copy of this documentation.

<img src="../assets/web.png" alt="droid Web Interface" class="zoom">

**Next**: [Connecting Raspberry Pi to the flight controller](connection.md).
