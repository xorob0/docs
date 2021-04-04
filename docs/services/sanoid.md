# Sanoid
[Sanoid](https://github.com/jimsalterjrs/sanoid/) is a tool to autmate snapshot on ZFS. I also use syncoid to upload some of my snapshots to `extra` as a quick backup.
## Config

```
[HDD1/Documents]
        frequently = 0
        hourly = 36
        daily = 30
        monthly = 3
        yearly = 1
        autosnap = yes
        autoprune = yes
[HDD1/Backups]
        frequently = 0
        hourly = 36
        daily = 30
        monthly = 3
        yearly = 1
        autosnap = yes
        autoprune = yes
[HDD1/Media]
        frequently = 0
        hourly = 36
        daily = 30
        monthly = 2
        yearly = 0
        autosnap = yes
        autoprune = yes
[extra/Documents]
        autoprune = yes
        frequently = 0
        hourly = 0
        daily = 90
        monthly = 12
        yearly = 0

        autosnap = no

        hourly_warn = 2880
        hourly_crit = 3600
        daily_warn = 48
        daily_crit = 60
[extra/Backups]
        autoprune = yes
        frequently = 0
        hourly = 0
        daily = 90
        monthly = 12
        yearly = 0

        autosnap = no

        hourly_warn = 2880
        hourly_crit = 3600
        daily_warn = 48
        daily_crit = 60
```

As for the cron jobs, I am using:

## Cron

```
* * * * * TZ=UTC /usr/sbin/sanoid --cron
0 3 * * * syncoid HDD1/Documents extra/Documents
0 3 * * * syncoid HDD1/Backups extra/Backups
```
This will take the automatic snapshots and move some to `extra` every days at 3AM
