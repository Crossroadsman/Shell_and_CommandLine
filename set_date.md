Setting the date
================

- Check status (systemd-based systems only):
  ```console
  $ timedatectl status
  ```

- Tell system to sync with NTP:
  ```console
  $ sudo timedatectl set-ntp on
  ```

- If NTP isn't available and need to set date manually:
  ```console
  $ sudo date -s "03 JAN 2018 10:00:00"
