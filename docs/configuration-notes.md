# Configuration Notes

## suricata.yaml
This is the main Suricata configuration file. It controls items such as the monitored
network, interface, rule locations, and logging.

## HOME_NET
Defines the local/internal networks that Suricata should consider part of the protected
environment.

## af-packet
Defines the network interface Suricata monitors. The interface must match the actual Kali
interface.

## Rule path
The lab uses:
```text
/var/lib/suricata/rules
```

## Custom rules
The custom rule file is:
```text
/etc/suricata/rules/local.rules
```
