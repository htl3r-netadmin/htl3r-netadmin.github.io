# NetAdmin

## Classes

### ssh.sshconnection.Connection

Die Klasse zum Aufbauen der SSH Verbindung. Hat methoden zum Verbinden und schließen der SSH Session und kann
kontrollieren ob Hosts UP oder DOWN sind.

``` python
Connection(host, username, password)
    .connect()
    .disconnect()
    .execute(command) # -> { "stdin": ..., "stdout": ..., "stderr" ... }
    .host_down()
```

### CheckStatus

Kontrolliert ob Gerät auf Pings antwortet und hat auch eine Loop-Funktion für regelmäßige Kontrollen.

```python
CheckStatus(timeout, interval, devices)
.start_loop()
.check_status_once()
```

### Settings

Liest die Settingsdatei (netadmin.json) ein und gibt die eingetragenen Devices an andere Klassen weiter.

```python
Settings(path)
.get_setting()
```

## netadmin.json

netadmin.json is the main configuration file. The following describes the options one by one:

```json
{
  "settings": {
    ...
  },
  "defaults": {
    "log-directory": "./dev-config",
    "fetch-interval": 10,
    "username": "netadmin",
    "password": "cisco",
    "ip": null,
    "type": null
  },
  "devices": [
    {
      ...
    },
    {
      ...
    }
  ]
}
```

* `settings`: here are the settings that NetAdmin will use
* `default`: here are the defaults for each device defined: if the parameter is not set for a given device it will
  default to this values
  * `log-directory`: here will be the running and startup configurations stored
  * `fetch-interval`: the interval in which NetAdmin will pull the data from a given device in seconds
  * `username`: the username NetAdmin will use to login to the device
  * `password`: the password NetAdmin will use to login to the device
  * `ip`: the IP-Address of the device
  * `type`: the type of the device (router / switch)
* `devices`: an array of the devices that NetAdmin will monitor
  * every option that can be configured in the defaults also can be overwritten here

## Database

```json
{
  "_id": "0b94879e16fb4094a3c2016a0a96b990",
  "_rev": "29-df520f907766b48ce8a9917b68923f5f",
  "created-at": 1620054614,
  "modified-at": 1620054614,
  "ip": "1.2.3.253",
  "type": "switch",
  "config": [
    {
      "config": "Current configuration : 3738 bytes\r\n!\r\n! Last configuration change at 15:05:44 UTC Mon May 3 2021 by netadmin\r\n!\r\nversion 15.6\r\nservice timestamps debug datetime msec\r\nservice timestamps log datetime msec\r\nservice password-encryption\r\n!\r\nhostname Demotest4\r\n!\r\nboot-start-marker\r\nboot-end-marker\r\n!\r\n!\r\nenable secret 5 $1$jA4k$QZ1Ouu/US2743jdtGWREi/\r\n!\r\naaa new-model\r\n!\r\n!\r\naaa authentication login default local\r\n!\r\n!\r\n!\r\n!\r\n!\r\naaa session-id common\r\nethernet lmi ce\r\n!\r\n!\r\n!\r\nmmi polling-interval 60\r\nno mmi auto-configure\r\nno mmi pvc\r\nmmi snmp-timeout 180\r\n!\r\n!\r\n!\r\n!\r\n!\r\nno ip icmp rate-limit unreachable\r\n!\r\n!\r\n!\r\n!\r\n!\r\n!\r\nno ip domain lookup\r\nip domain name NetAdmin\r\nip cef\r\nno ipv6 cef\r\n!\r\nmultilink bundle-name authenticated\r\n!\r\n!\r\n!\r\n!\r\nusername netadmin privilege 15 secret 5 $1$CUa7$6t8kgF4oIVVFO.Cv0psZx.\r\n!\r\nredundancy\r\n!\r\nno cdp log mismatch duplex\r\n!\r\nip tcp synwait-time 5\r\n! \r\n!\r\n!\r\n!\r\n!\r\n!\r\n!\r\n!\r\n!\r\n!\r\n!\r\n!\r\n!\r\ninterface GigabitEthernet0/0\r\n no ip address\r\n shutdown\r\n duplex auto\r\n speed auto\r\n media-type rj45\r\n!\r\ninterface GigabitEthernet0/1\r\n description toRouter2\r\n ip address 1.2.3.253 255.255.255.0\r\n duplex auto\r\n speed auto\r\n media-type rj45\r\n!\r\ninterface GigabitEthernet0/2\r\n description to192.168.0.1Netw\r\n no ip address\r\n duplex full\r\n speed 1000\r\n media-type rj45\r\n!\r\ninterface GigabitEthernet0/2.99\r\n encapsulation dot1Q 99\r\n ip address 192.168.0.254 255.255.255.0\r\n!\r\ninterface GigabitEthernet0/3\r\n no ip address\r\n shutdown\r\n duplex auto\r\n speed auto\r\n media-type rj45\r\n!\r\nrouter ospf 10\r\n network 1.2.3.0 0.0.0.255 area 10\r\n network 192.168.0.0 0.0.0.255 area 10\r\n!\r\nip forward-protocol nd\r\n!\r\n!\r\nno ip http server\r\nno ip http secure-server\r\nip ssh version 2\r\n!\r\n!\r\n!\r\n!\r\n!\r\n!\r\ncontrol-plane\r\n!\r\nbanner exec ^C\r\n**************************************************************************\r\n* IOSv is strictly limited to use for evaluation, demonstration and IOS  *\r\n* education. IOSv is provided as-is and is not supported by Cisco's      *\r\n* Technical Advisory Center. Any use or disclosure, in whole or in part, *\r\n* of the IOSv Software or Documentation to any third party for any       *\r\n* purposes is expressly prohibited except as otherwise authorized by     *\r\n* Cisco in writing.                                                      *\r\n**************************************************************************^C\r\nbanner incoming ^C\r\n**************************************************************************\r\n* IOSv is strictly limited to use for evaluation, demonstration and IOS  *\r\n* education. IOSv is provided as-is and is not supported by Cisco's      *\r\n* Technical Advisory Center. Any use or disclosure, in whole or in part, *\r\n* of the IOSv Software or Documentation to any third party for any       *\r\n* purposes is expressly prohibited except as otherwise authorized by     *\r\n* Cisco in writing.                                                      *\r\n**************************************************************************^C\r\nbanner login ^C\r\n**************************************************************************\r\n* IOSv is strictly limited to use for evaluation, demonstration and IOS  *\r\n* education. IOSv is provided as-is and is not supported by Cisco's      *\r\n* Technical Advisory Center. Any use or disclosure, in whole or in part, *\r\n* of the IOSv Software or Documentation to any third party for any       *\r\n* purposes is expressly prohibited except as otherwise authorized by     *\r\n* Cisco in writing.                                                      *\r\n**************************************************************************^C\r\n!\r\nline con 0\r\n exec-timeout 0 0\r\n privilege level 15\r\n password 7 104D000A0618\r\n logging synchronous\r\nline aux 0\r\n exec-timeout 0 0\r\n privilege level 15\r\n logging synchronous\r\nline vty 0 4\r\n password 7 030752180500\r\n transport input ssh\r\nline vty 5 15\r\n password 7 030752180500\r\n transport input ssh\r\n!\r\nno scheduler allocate\r\n!\r\nend\r\n\r\nDemotest4#",
      "created-at": 1620054614
    }
  ],
  "uptime": [
    {
      "created-at": 1620054614,
      "state": false
    }
  ],
  "data": { ... }
}
```

* `_id`: unique id of a device
* `_rev`: revision number; consists of: number of changes + "-" + "random string"
* `created-at`: when was this entry created
* `modified-at`: when was this entry last modified
* `ip`: IP of the device
* `type`: type of the device (switch | router | pc | server)
* `config`: list of fetched configurations
  * `config`: the configuration pulled from the device
  * `created-at`: timestamp of the fetch (in seconds)
* `uptime`: list of statechanges of the device (when the device went online and offline)
  * `created-at`: time of check
  * `state`: state of the device at the given time (True -> Online, False -> Offline)
* `data`: device specific data (depends on which type this device is)