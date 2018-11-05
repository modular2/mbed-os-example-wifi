# mbed-os-example-wifi #

Wi-Fi example for Mbed OS

## Getting started with the Wi-Fi API ##

This is an example of a Wi-Fi application using the Wi-Fi and network socket APIs that [Mbed OS](https://github.com/ARMmbed/mbed-os) provides.

The program brings up the Wi-Fi and the underlying network interface and uses it to scan available networks, connects to a network, prints interface and connection details and performs an HTTP operation.

For more information about Wi-Fi APIs, please visit the [Mbed OS Wi-Fi](https://os.mbed.com/docs/latest/reference/wi-fi.html) documentation.

### Supported hardware ###

* All Mbed OS boards with build-in Wi-Fi module:
* Boards with external WiFi shields, Modular-2 with ESP-12F(esp8266) module using pins PB_6(tx) and PB_7(rx). 

##  Getting started ##

1. Import the example.

   ```
   mbed import https://github.com/maximlab/mbed-os-example-wifi
   cd mbed-os-example-wifi
   ```

1. Configure the Wi-Fi shield and settings.

   Edit ```mbed_app.json``` to include the correct Wi-Fi shield, SSID and password:
<pre><code>
{
    "config": {
        "wifi-ssid": {
            "help": "WiFi SSID",
            "value": "\"SSID\""
        },
        "wifi-password": {
            "help": "WiFi Password",
            "value": "\"PASSWORD\""
        }
    },
    "target_overrides": {
        "*": {
            "platform.stdio-convert-newlines": true,
            "esp8266.provide-default" : true,
            "drivers.uart-serial-rxbuf-size"    : 1024,
            "drivers.uart-serial-txbuf-size"    : 1024,
            "esp8266.rx"                        : "PB_7",
            "esp8266.tx"                        : "PB_6",
            "nsapi.default-wifi-security"       : "WPA_WPA2"
        }
    }
}
</code></pre>

1. Compile and generate binary.
    For example, for `GCC`:
    ```
    mbed compile -t GCC_ARM -m NUCLEO_F429ZI
    ```

1. Open a serial console session with the target platform using the following parameters:
    * **Baud rate:** 9600
    * **Data bits:** 8
    * **Stop bits:** 1
    * **Parity:** None

1. Copy or drag the application `mbed-os-example-wifi.bin` in the folder `mbed-os-example-wifi/BUILD/<TARGET NAME>/<PLATFORM NAME>` onto the target board.

1. The serial console should display a similar output to below, indicating a successful Wi-Fi connection:
    ```
    WiFi example

    Scan:
    Network: Dave Hot Spot secured: Unknown BSSID: 00:01:02:03:04:05 RSSI: -58 Ch: 1
    1 network available.

    Connecting...
    Success

    MAC: 00:01:02:03:04:05
    IP: 192.168.0.5
    Netmask: 255.255.255.0
    Gateway: 192.168.0.1
    RSSI: -27

    Sending HTTP request to www.arm.com...
    sent 38 [GET / HTTP/1.1]
    recv 64 [HTTP/1.1 301 Moved Permanently]

    Done
    ```


