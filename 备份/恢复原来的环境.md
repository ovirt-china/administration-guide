# 恢复原来的环境

若数据库是从来未使用过的或者全新安装的，请使用如下命令初始化数据库服务：


    # service postgresql initdb
    # service postgresql start
    # chkconfig postgresql on




    #su postgres
    $dropdb engine;



创建数据库用户以及数据库：


    postgres=# create role [user name] with login encrypted password '[password]';
    postgres=# CREATE DATABASE [database name] OWNER [user name] template template0 encoding 'UTF8' lc_collate 'en_US.UTF-8' lc_ctype 'en_US.UTF-8';
    # [password] 是/etc/ovirt-engine/engine.conf.d/10-setup-database.conf中的数据库密码.
    # [database name] 和 [user name] 默认情况下是engine



如果数据库是全新安装的或者之前未曾配置该步骤的的，编辑文件
/var/lib/pgsql/data/pg\_hba.conf，并在紧接着以 Local
开头的那一行下面添加如下内容：


    host [database name] [user name] 0.0.0.0/0 md5
    host [database name] [user name] ::0/0 md5



恢复数据库：


    #service postgresql restart
    #cd [your backup parent directory]
    #engine-backup --mode=restore --file=backup --log=engine-backup.log --change-db-credentials --db-host=localhost --db-name=[database name] --db-user=[user name] --db-password



恢复配置文件：


    #tar -jxvf backup
    #cd files
    #mv /etc/pki/ovirt-engine/ /etc/pki/ovirt-engine.backup
    #cp -rvcpf pki/ovirt-engine/ /etc/pki/
    #mv /etc/httpd/conf.d/ conf.d.backup
    # cp -vrcpf httpd/conf.d/ /etc/httpd/
    #mv /etc/ovirt-engine ovirt-engine.backup
    #cp -vrcfp ovirt-engine /etc/




    #service ovirt-engine restart
    #service httpd restart



