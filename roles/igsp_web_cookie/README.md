igsp\_web\_cookie
=================

Role for installing and configuring [igsp\_web\_cookie](https://github.com/Duke-GCB/igsp_web_cookie)

Depends on [oracle_instantclient](../oracle_instantclient)

For igsp\_web\_cookie to function properly, all servers in an environment (dev/test/prod) must use the same database and key pair. These environments are _groups_ in ansible: cookiedev, cookietest, cookieprod, and the configurations for these groups are encrypted in [group_vars](../../group_vars).

[defaults/main.yml](defaults/main.yml) has placeholders for variables that must be specified. Some should be overridden by group_vars, and some may be overridden at runtime:

`ansible-playbook ... --extra-vars "igsp_web_cookie.owner=apache"`
