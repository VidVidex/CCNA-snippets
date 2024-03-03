# Device Discovery

## CDP (Cisco Discovery Protocol)

- Cisco proprietary

### Enable CDP <globally

```txt
Router(config)# cdp run
```

### Disable CDP globally

```txt
Router(config)# no cdp run
```

### Enable CDP on an interface

```txt
Router(config)# interface g0/0
Router(config-if)# cdp enable
```

### Disable CDP on an interface

```txt
Router(config)# interface g0/0
Router(config-if)# no cdp enable
```

### Usage of CDP

```txt
Router# show cdp
Router# show cdp neighbors
Router# show cdp neighbors detail
```

## LLDP (Link Layer Discovery Protocol)

- open standard

### Enable LLDP globally

```txt
Router(config)# lldp run
```

### Disable LLDP globally

```txt
Router(config)# no lldp run
```

### Enable LLDP on an interface

```txt
Router(config)# interface g0/0
Router(config-if)# lldp transmit
Router(config-if)# lldp receive
```

### Disable LLDP on an interface

```txt
Router(config)# interface g0/0
Router(config-if)# no lldp transmit
Router(config-if)# no lldp receive
```

### Usage of LLDP

```txt
Router# show lldp
Router# show lldp neighbors
Router# show lldp neighbors detail
```
