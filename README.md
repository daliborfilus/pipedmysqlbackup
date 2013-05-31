# DB Backup

Simple tool for backing up mysql databases, using mysqldump
(with --single-transaction argument for non-blocking backups),
gzip, separating backups to different directories.
Can do cleanup of old backups.

## Installation and usage

- Copy to the database server via SSH or similar.
- Ensure that the script is executable (`chmod u+x ./db_backup`).
- Copy `db_backup.conf.template` to `db_backup.conf` and update corresponding values.
  This file must be in the same directory as the backup script (for now).
- Insert this script to crontab (using `crontab -e` or similar).

### Crontab examples

    #m h dom mon dow command
    # run daily backup every day
    0 2 * * * /usr/local/bin/db_backup daily >> /var/log/db_backup.log
    # cleanup old backups every day
    0 3 * * * /usr/local/bin/db_backup cleanup >> /var/log/db_backup.log
    # run weekly backup on sunday
    0 4 1 * 0 /usr/local/bin/db_backup weekly >> /var/log/db_backup.log
    # run monthly tasks 1st in the month
    0 4 1 * * /usr/local/bin/db_backup monthly >> /var/log/db_backup.log

## Dependencies

- mysqlclient (for mysqldump)
- gzip

## License

MIT
