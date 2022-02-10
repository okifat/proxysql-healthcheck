# Proxysql-healtcheck

## Run healthceck with supervisor
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

## How to build and release

Run the init command to create an example .goreleaser.yaml file

```
goreleaser init
```

Now, lets run a "local-only" release to see if it works using the release command:

```
goreleaser release --snapshot --rm-dist
```

In order to release to GitHub, you'll need to export a GITHUB_TOKEN environment variable, which should contain a valid GitHub token with the repo scope. It will be used to deploy releases to your GitHub repository. You can create a new github token here.

```
export GITHUB_TOKEN="YOUR_GH_TOKEN"
```

GoReleaser will use the latest Git tag of your repository.

Now, create a tag and push it to GitHub:

```
git tag -a v0.1.0 -m "First release"
git push origin v0.1.0
```

Now you can run GoReleaser at the root of your repository:

```
goreleaser release
```

That's all it takes!

