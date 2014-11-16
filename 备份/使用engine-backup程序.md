# 使用engine-backup程序

*简要说明*.
数据是一定不能丢的，OVIRT开发此脚本程序帮助您实现这一目标。

engine-backup是将备份和恢复统一到一起的程序，根据用户的参数而做区别。

先来查看engine-backup的使用帮助：


     engine-backup --help
    engine-backup: backup and restore ovirt-engine environment
    USAGE:
        /usr/bin/engine-backup [--mode=MODE] [--scope=SCOPE] [--file=FILE] [--log=FILE]
     MODE is one of the following:
        backup                  backup system into FILE
        restore                 restore system from FILE
     SCOPE is one of the following:
        all                     complete backup/restore (default)
        db                      database only
     --file=FILE                file to use during backup or restore
     --log=FILE                 log file to use
     --change-db-credentials    activate the following options, to restore
                                the database to a different location etc.
                                If used, existing credentials are ignored.
     --db-host=host             set database host
     --db-port=port             set database port
     --db-user=user             set database user
     --db-passfile=file         set database password - read from file
     --db-password=pass         set database password
     --db-password              set database password - interactively
     --db-name=name             set database name
     --db-secured               set a secured connection
     --db-secured-validation    validate host



以下是使用全部参数的例子：


     engine-backup --mode=backup --scope=all --file=backup --log=backup.log --change-db-credentials --db-host=localhost --db-port=5432 --db-user=engine --db-password=ffdC9lhX --db-name=engine
    Backing up...
    Done.



将backup这个文件，放到您的备份环境中，最好是远程的。

> **Note**
>
> backup是经过tar,bzip2打包的，所以您打算手动查看请使用如下命令行：
>
>
>     tar -jxvf backup
>
>

