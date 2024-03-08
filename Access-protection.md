# Access protection

In the following examples I'll use `cisco123` as the password.
You should use something stronger.

## Securing privileged exec mode

```txt
Router(config)# enable secret cisco123
```

## Securing user exec (console ports)

```txt
# Without this the password will be visible in plain text
Router(config)# service password-encryption 

Router(config)# line console 0
Router(config-line)# password cisco123   
Router(config-line)# login
```
