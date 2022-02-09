# proxysql-healtcheck

##Setting healthceck with supervisor
```
[program:proxysql-healthcheck]
command=/opt/proxysql_healthcheck/proxysql-healthcheck {{ mysql_user }} {{ mysql_pass }} {{ hosts_server }}:port dbname
directory=/opt/proxysql_healthcheck
process_name=%(program_name)s
numprocs=1
umask=022
priority=1
user=root
group=root
autostart=true
autorestart=true
redirect_stderr=true
stdout_logfile=/var/log/supervisor/proxysql-healthcheck.log
```


