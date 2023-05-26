# Switch (L2) security

## Port security

- disable unused ports

```txt
Switch(config)# interface range g0/1-24     # Select all 24 ports
Switch(config-if-range)# shutdown           #  and shut them down
```

- enable port security

```txt
Switch(config)# interface g0/1
Switch(config-if)# switchport mode access    # port security only works in access mode
Switch(config-if)# switchport port-security
```

- set maximum number of MAC addresses

```txt
Switch(config-if)# switchport port-security maximum 2   # max 2 MAC addresses allowed on this port
```

- configure allowed MAC addresses
  - manually

    ```txt
    Switch(config-if)# switchport port-security mac-address 0000.1111.2222
    ```

  - dynamically

    ```txt
    # Switch will learn MAC addresses from the first 2 (configured above) devices 
    # that connect to this port and save them
    # (without sticky, they will be lost after a reboot)
    Switch(config-if)# switchport port-security mac-address sticky
    ```

- configure port aging

```txt
# Remove MAC addresses from the port's secure address table after 60 seconds of inactivity
Switch(config-if)# switchport port-security aging type inactivity
Switch(config-if)# switchport port-security aging time 60
```

- configure violation mode

```txt
# Shutdown port if violation occurs (other options: restrict, protect)
Switch(config-if)# switchport port-security violation shutdown
```

## DHCP snooping

The following enables DHCP snooping on VLANs 5 and 10, configures `fa0/1` as a trusted port, and limits the number of DHCP packets on ports `fa0/2` to `fa0/24` to 5 per second.

```txt
Switch(config)# ip dhcp snooping
Switch(config)# ip dhcp snooping vlan 5,10

Switch(config)# interface f0/1
Switch(config-if)# ip dhcp snooping trust
Switch(config-if)# exit

Switch(config)# interface range f0/2 - 24
Switch(config-if-range)# ip dhcp snooping limit rate 5
Switch(config-if-range)# exit
```

Verify:

```txt
Switch# show ip dhcp snooping
Switch# show ip dhcp snooping binding
```

## Dynamic ARP inspection (DAI)

- requires DHCP snooping

The following enables DAI on VLAN 10, configures `fa0/1` as a trusted port.

```txt
Switch(config)# ip dhcp snooping
Switch(config)# ip dhcp snooping vlan 10
Switch(config)# ip arp inspection vlan 10

Switch(config)# interface fa0/1
Switch(config-if)# ip dhcp snooping trust
Switch(config-if)# ip arp inspection trust
```

## Configure PortFast

- only on access ports facing end devices, never on switch-to-switch links

The following enables PortFast on ports `fa0/2` to `fa0/24`.

```txt
Switch(config)# interface range f0/2 - 24
Switch(config-if-range)# spanning-tree portfast
```

Alternatively, you can enable PortFast by default on all access ports:

```txt
Switch(config)# spanning-tree portfast default
```

## Configure BPDU guard

```txt
Switch(config)# interface range f0/2 - 24
Switch(config-if-range)# spanning-tree bpduguard enable
```

Or by default on all ports:

```txt
Switch(config)# spanning-tree portfast bpduguard default
```
