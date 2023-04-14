# VLANs

## Creating a new VLAN

```txt
Switch(config)# vlan <VLAN_ID>
Switch(config-vlan)# name <NAME>
```

Example:

```txt
Switch(config)# vlan 10
Switch(config-vlan)# name ACCOUNTING
```

Verify:

```txt
Switch# show vlan brief
```

## Deleting a VLAN

```txt
Switch(config)# no vlan <VLAN_ID>
```

Deleting all VLANs (deletes entire VLAN database)

```txt
Switch(config)# delete flash:vlan.dat
```

## Set interface to access mode (for end devices)

```txt
Switch(config)# interface <INTERFACE_ID>
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan <VLAN_ID>
```

Example:

```txt
Switch(config)# interface fa0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10
```

Verify:

```txt
Switch# show vlan brief
```

## Set interface to trunk mode (for connections between switches)

```txt
Switch(config)# interface <INTERFACE_ID>
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan <VLAN_IDs>
Switch(config-if)# switchport trunk native vlan <VLAN_ID>
```

Example:

```txt
Switch(config)# interface fa0/1
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan 10,20
Switch(config-if)# switchport trunk native vlan 100
```

Verify:

```txt
Switch# show interface trunk
```
