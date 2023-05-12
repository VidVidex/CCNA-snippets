# DHCPv4

![DHCPv4 topology](img/dhcp.png)

## Router0 as DHCP server

```txt

# Exclude addresses that you want to assign statically (from - to)
Router0(config)# ip excluded-address 192.168.1.1 192.168.1.20

# Create a pool, you can name it anything you want
Router0(config)# ip dhcp pool POOL_NAME

# Set configuration options, networka and default-router are mandatory 
Router0(dhcp-config)# network 192.168.1.0 255.255.255.0
Router0(dhcp-config)# default-router 192.168.1.1
Router0(dhcp-config)# dns-server 8.8.8.8
Router0(dhcp-config)# domain-name example.net
...
```

## Verify DHCP configuration

```txt
Router0# show ip dhcp bindings
Router0# show ip dhcp server statistics
```

## Helper address

If you don't want your DHCP server to be on your router but rather a dedicated machine or a router somewhere else on the network you'll need to configure a `helper-address`. (DHCP packets are broadcasts and therefore aren't sent from one network to another).

Configuring `Router0` to forward DHCP packets from `Server0` to the PCs:

```txt
# Go to the interface facing towards the PCs
Router0(config)# interface g0/0

# Create a helper address (192.168.1.10 is Server0's IP)
Router0(config-if)# ip helper-address 192.168.1.10
```

## Interface as a DHCP client

If you want an interface to obtain an IP address via DHCP

```txt
Router0(config)# interface g0/0
Router0(config)# ip address dhcp
```
