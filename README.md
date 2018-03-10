## Server Tools
Some random tools for my servers.

Scripts available for:
* Dell R510

### dellfanctl
Controlling DELL server FANs with a script using IMPI
#### Usage:
* No arguments
```
root@freenas:~ # ./dellfanctrl
Dell R510 FAN control script v1.0
There is not enough parameters for this script!

Example usage:
Enable automatic FAN control:           ./dellfanctrl auto
Disable automatic FAN control:          ./dellfanctrl manual
Disable & set speed to N percents:      ./dellfanctrl set 10
```

* Enable auto mode
```
root@freenas:~ # ./dellfanctrl auto
Dell R510 FAN control script v1.0
Running: ipmitool raw 0x30 0x30 0x01 0x01

Command executed successfully
```

* Enable manual mode
```
root@freenas:~ # ./dellfanctrl manual
Dell R510 FAN control script v1.0
Running: ipmitool raw 0x30 0x30 0x01 0x00

Command executed successfully
```

* Set speed to 8 percents (ignore error - it still works fine)
```
root@freenas:~ # ./dellfanctrl set 8
Dell R510 FAN control script v1.0
Setting FAN speed to 8%
Running: ipmitool raw 0x30 0x30 0x02 0xff 0x08
Unable to send RAW command (channel=0x0 netfn=0x30 lun=0x0 cmd=0x30 rsp=0xcc): Invalid data field in request
Execution failed with status 1
```

* Status:
```
root@freenas:~ # ./dellfanctrl status
Dell R510 FAN control script v1.0
Current system status:
Ambient Temp      23.000
FAN MOD 1A RPM    2160.000
FAN MOD 2A RPM    2160.000
FAN MOD 3A RPM    2160.000
FAN MOD 4A RPM    2160.000
Fan Redundancy    0x0
Mem Overtemp      0x0
FAN MOD 5A RPM    2160.000
```
