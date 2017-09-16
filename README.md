Simple cron job for Borg
========================

This script is a simple file that can be dropped in
`/etc/cron.daily/borg` on Linux systems that support such a
directory. Alternatively, it can be launched as a commandline script
to execute your backup policies.

This script will run borg backups with a predefined exclusion list and
some options. Policies are defined in the script itself and it is not
designed to be ran without manual configuration and a full review of
the script.

It will also check to see if the external drive is mounted
beforehand, to avoid filling up /media with a new backup, filling up
the / directory.

This script should not exist. There should instead be a borg cron
subcommand that reads a config file and "borg cron" would then do the
right thing. That would need to be implemented in `borg/archiver.py`,
with a hook in `run()` and a `def do_cron()` that would call
`do_create()` and others. Unfortunately, upstream has showed hostility
towards the idea (see [#315](https://github.com/borgbackup/borg/issues/315#issuecomment-149545564)) so yours truly gave up in trying to
help everyone and just scratched his own itch instead, which seems to
be what we do around here anyways.

see also:

* https://github.com/borgbackup/borg/issues/315
* https://github.com/borgbackup/borg/issues/271
* https://github.com/borgbackup/borg/issues/326

This was originally written to replace bup, or more precisely, my
wrapper named [bup-cron](https://gitlab.com/anarcat/bup-cron/). There are still some features missing
from bup-cron, namely:

 * filesystem snapshots
 * parity blocks
 * syslog - support still missing from borg, although a logging config
   file could be written to send stuff to syslog there's no --syslog flag
 * timing information, although --stats does some of that

... but I don't really need those features right now, as I do not run
entreprise level backups anymore: I just do my personal backups with
borg. But obviously, all this stuff would be required for a more
serious borg deployment.
