# NTP (Network Time Protocol)

- UDP 123

## Show clock

```txt
Router# show clock
```

## Set clock

```txt
Router(config)# clock set HH:MM:SS MONTH DAY YEAR

# Example
Router(config)# clock set 13:32:00 23 July 1997
```

## Set NTP server

```txt
Router(config)# ntp server IP_ADDRESS

# Example
Router(config)# ntp server 193.2.4.2
```

## Verify NTP

```txt
Router# show ntp status
Router# show ntp associations
```
