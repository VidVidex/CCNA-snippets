# Password Recovery

1. Enter ROMMON

   - Turn off the router
   - Turn on the router
   - Press the `Break` key to enter ROMMON (Putty: right-click on the title bar and select `Special Commands` -> `Break`)

2. Change the configuration register

    ```txt
    rommon 1 > confreg 0x2142
    rommon 2 > reset
    ```

3. Copy running-config to startup-config
    - This **will erase** all configuration on the router
    - If you don't want to erase the configuration copy startup-config to running-config, change password, and then copy running-config to startup-config instead of the following command

    ```txt
    Router# copy running-config startup-config
    ```

4. Reset configuration register

    ```txt
    Router(config)# config-register 0x2102
    ```

5. Reload

    ```txt
    Router# reload
    ```
