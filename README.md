Simple cron job for Borg
========================

This script is a simple file that can be dropped in
`/etc/cron.daily/borg` on Linux systems that support such a
directory. Alternatively, it can be launched as a commandline script
to execute your backup policies.

Policies are defined in the script itself and it is not designed to be
ran without manual configuration and a full review of the script. This
was created only because upstream didn't seem open to the possibility
of writing this directly in Borg itself, otherwise this would have
been implemented as a `cron` subcommand in borg.
