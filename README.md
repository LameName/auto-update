# Auto-Update

Auto-Update is a systemd service, systemd timer and shell script to *fully* update the system and reboot the machine as necessary. It is intended to close the gap after "automatically install security updates", where other updates are not applied automatically and the user must figure out what to do.

We can partially sidestep users by automatically installing security updates. However, distros still prompt users for non-security updates, and many non-technical users don't know what the prompt is or what they should do. This is a usablity problem that many distros have not addressed.

In addition, some security updates are misclassified and not installed automatically. Misclassifying an update happens more often than you expect. Updates are labeled security if the vulnerability was obvious or someone provided a working exploit. Many design problems and memory errors are not investigated and lack an exploit, so they just get fixed and labeled as non-security. Those that are fixed without investigation must be installed manually by the user.

## Setup

You should run `install.sh` to install the service. The service runs on Armbian, CentOS, Debian, Fedora, Linaro, Red Hat, Ubuntu and Zorin.

```
sudo ./install.sh
```

## Service status

Once the files are copied and the service and timer are enabled, you can check the status with the following commands. The timer should show `enabled`, and `active (waiting)`.

```
$ systemctl status auto-update.timer
● auto-update.timer - Run auto-update.service once a day
   Loaded: loaded (/etc/systemd/system/auto-update.timer; enabled; vendor prese>
   Active: active (waiting) since Tue 2019-06-18 10:41:42 EDT; 6min ago
   Trigger: Wed 2019-06-19 05:02:25 EDT; 18h left
```

You can also use `systemctl list-timers` to show the status of all timers on the system.

## Cron jobs

You should be able to schedule `/usr/sbin/auto-update` as a cron job under the system account. The script `install-cron.sh` will install `auto-update.dnf` or `auto-update.apt` as `/usr/sbin/auto-update` in `/etc/cron.daily`.
