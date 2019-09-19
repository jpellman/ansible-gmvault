ansible-gmvault
=========

A role that installs gmvault and populates crontabs with cronjobs that regularly back up emails for a given user or set of users.
Multiple cronjobs can be defined for different intervals and to differentiate between full/incremental backups.

Requirements
------------

Built-in Ansible modules should be sufficient to run this role.  This role has not yet been tested with a specific version of Ansible as of 9/19/19.

Role Variables
--------------

Role variables are described in more detail in comments under _defaults/main.yml_.

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
