# Nagios / Icinga check for pgBackRest

This plugin parses the output of `pgbackrest info --output json` and checks if the backup archive contains a specific number of backups of a given type. E.g., between 1 and 2 full backups, 4 to 8 differential backups and at least 2 incremental backups.

It's also capable of doing ageing checks of backups. E.g., check if the newest incremental backup is not older than 3600 seconds.

# Python Requirements

    - python3
    - argparse
	- nagiosplugin
	- json

# Usage

```
$ check_pgbackrest --help
usage: check_pgbackrest [-h] -s STANZA [-wf RANGE] [-cf RANGE] [-wd RANGE]
                        [-cd RANGE] [-wi RANGE] [-ci RANGE] [-wnfa RANGE]
                        [-cnfa RANGE] [-wofa RANGE] [-cofa RANGE]
                        [-wnda RANGE] [-cnda RANGE] [-woda RANGE]
                        [-coda RANGE] [-wnia RANGE] [-cnia RANGE]
                        [-woia RANGE] [-coia RANGE] [-b STANZA] [-d]

Icinga / Nagios check for pgBackRest.

optional arguments:
  -h, --help            show this help message and exit
  -s STANZA, --stanza STANZA
                        return warning if the number of full backups is
                        outside RANGE
  -wf RANGE, --warning-full RANGE
                        return warning if the number of full backups is
                        outside RANGE
  -cf RANGE, --critical-full RANGE
                        return critical if the number of full backups is
                        outside RANGE
  -wd RANGE, --warning-diff RANGE
                        return warning if the number of differential backups
                        is outside RANGE
  -cd RANGE, --critical-diff RANGE
                        return critical if the number of differential backups
                        is outside RANGE
  -wi RANGE, --warning-incr RANGE
                        return warning if the number of incremental backups is
                        outside RANGE
  -ci RANGE, --critical-incr RANGE
                        return critical if the number of incremental backups
                        is outside RANGE
  -wnfa RANGE, --warning-newest-full-age RANGE
                        return warning if the age of the newest full backup is
                        outside RANGE (seconds)
  -cnfa RANGE, --critical-newest-full-age RANGE
                        return critical if the age of the newest full backup
                        is outside RANGE (seconds)
  -wofa RANGE, --warning-oldest-full-age RANGE
                        return warning if the age of the oldest full backup is
                        outside RANGE (seconds)
  -cofa RANGE, --critical-oldest-full-age RANGE
                        return critical if the age of the oldest full backup
                        is outside RANGE (seconds)
  -wnda RANGE, --warning-newest-diff-age RANGE
                        return warning if the age of the newest diff backup is
                        outside RANGE (seconds)
  -cnda RANGE, --critical-newest-diff-age RANGE
                        return critical if the age of the newest diff backup
                        is outside RANGE (seconds)
  -woda RANGE, --warning-oldest-diff-age RANGE
                        return warning if the age of the oldest diff backup is
                        outside RANGE (seconds)
  -coda RANGE, --critical-oldest-diff-age RANGE
                        return critical if the age of the oldest diff backup
                        is outside RANGE (seconds)
  -wnia RANGE, --warning-newest-incr-age RANGE
                        return warning if the age of the newest incr backup is
                        outside RANGE (seconds)
  -cnia RANGE, --critical-newest-incr-age RANGE
                        return critical if the age of the newest incr backup
                        is outside RANGE (seconds)
  -woia RANGE, --warning-oldest-incr-age RANGE
                        return warning if the age of the oldest incr backup is
                        outside RANGE (seconds)
  -coia RANGE, --critical-oldest-incr-age RANGE
                        return critical if the age of the oldest incr backup
                        is outside RANGE (seconds)
  -b STANZA, --binary STANZA
                        path to pgbackrest binary
  -d, --debug           print debug output
```

## Check the number of full backups:

    1. sudo -u postgres check-pgbackrest/check_pgbackrest --stanza main --warning-full 2:2 --critical-full 1:2
       PGBACKREST OK - full_backups is 2 | diff_backups=2 full_backups=2;2:2;1:2
    2. sudo -u postgres check-pgbackrest/check_pgbackrest --stanza main --warning-full 2:2 --critical-full 1:2 --warning-diff 1:1
       PGBACKREST WARNING - diff_backups is 2 (outside range 1:1) | diff_backups=2;1:1 full_backups=2;2:2;1:2


# License

This project uses the MIT Licence.
