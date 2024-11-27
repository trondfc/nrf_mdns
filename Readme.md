## Setup
WiFi ssid and password are set in `prj.conf` for both the responder and resolver.
Responder hostname is set in `overlay-responder.conf` and resolver query in `overlay-resolver.conf`. These two should be the same.
After flashing the devices, the devices should be connected to the same network. For testing purposes the mDNS queries is sent after pushing button 1 on the resolver. 

## Building
### Responder
The device responding to local mndns queries. 
```
west build -p -b nrf5340_audio_dk/nrf5340/cpuapp -d build_responder --sysbuild -- -DSHIELD=nrf7002ek  -DEXTRA_CONF_FILE="overlay-responder.conf" && west flash -d build_responder
```


### Resolver
The device 
```
west build -p -b nrf5340_audio_dk/nrf5340/cpuapp -d build_resolver --sysbuild -- -DSHIELD=nrf7002ek  -DEXTRA_CONF_FILE="overlay-resolver.conf" && west flash -d build_resolver
```

## TODO
- Zephyr mDNS has had a rewrite allowing for responder and resolver to be in the same application [github](https://github.com/zephyrproject-rtos/zephyr/pull/73422). This change is not yet in ncs sdk 2.7.0 (using sdk-zephyr v3.6.99) but should be in 2.8.0 (using sdk-zephyr v3.7.99)

## Sources
- [nrf mDNS responder](https://docs.nordicsemi.com/bundle/ncs-2.7.0/page/zephyr/samples/net/mdns_responder/README.html)
- [nrf mDNS resolver](https://docs.nordicsemi.com/bundle/ncs-2.1.1/page/zephyr/samples/net/dns_resolve/README.html#dns-resolve-sample)
- [nrf wifi station](https://docs.nordicsemi.com/bundle/ncs-latest/page/nrf/samples/wifi/sta/README.html)