ansible-gmvault
=========

A role that installs gmvault and populates crontabs with cronjobs that regularly back up emails for a given user or set of users.
Multiple cronjobs can be defined for different intervals and to differentiate between full/incremental backups.

Requirements
------------

Built-in Ansible modules should be sufficient to run this role.  This role has not yet been tested with a specific version of Ansible as of 9/19/19.

Role Variables
--------------

 The variables below are used to define default arguments for when cron jobs that invoke gmvault are run.  They are ignored if no cron jobs are defined. They can be overridden by defining a corresponding variable in one of the  named crons in `gmvault_cron_list` below. 

```
gmvault_cron_default_minute: "0"
gmvault_cron_default_hour: "4"
gmvault_cron_default_day: "*"
gmvault_cron_default_month: "*"
gmvault_cron_default_weekday: "*" 
```

`gmvault_cron_list` should be populated with a list of dictionaries.  Each dictionary in the list should contain values indicating which flags should be passed to gmvault for a cron job or cron jobs that invoke gmvault automatically.

For flags that accept arguments the value should be the corresponding argument.  For flags that represent booleans, `True` should be added to indicate that the flag should be appended to the gmvault command. Omitting a flag from the list will have the same result as setting that boolean flag to `False`, which is to omit that flag entirely from the command syntax.

If `gmvault_cron_list` is undefined, no crons will be added and gmvault will just be installed.

Note that as of 3/31/19, you'll have to implement one of the workarounds indicated [here](https://github.com/gaubert/gmvault/issues/335#issuecomment-475435935) or [here](https://github.com/gaubert/gmvault/issues/335#issuecomment-475437988), unless you're at a college/university for some reason (because $logic).

If you opt to use an app password, the Ansible playbook will run `gmvault sync --store-passwd <email>` before creating the crons to store your credentials.  This behavior can be overridden by defining a variable `gmvault_store_passwd` and setting it to `False`.

```
gmvault_cron_list:
    - name: Monthly
      type: full
      db_dir: /path/to/mycustom-gmvault-db
      oauth2: False
      password: <password encrypted with vault>
      imap_req: False
      gmail_req: False
      emails_only: False
      chats_only: False
      encrypt: False
      check_db: "no"
      multiple_db_owner: False
      no_compression: False
      server: imap.gmail.com
      port: 993
      address: user@example.com
      user: user_whose_crontab_this_should_be_in
      minute: "0"
      hour: "0"
      day: "1"
      month: "*/4"
      weekday: "*"
```

Dependencies
------------

None.

Example Playbook
----------------

TODO

License
-------

GPLv3

Author Information
------------------

Written by John Pellman to satisfy his own datahoarding instincts in September 2019.  John can be contacted at <lastname> dot <firstname> at gmail dot com (of course) and his website is [https://libjpel.so](https://libjpel.so).
