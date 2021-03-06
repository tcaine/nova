===========
nova-manage
===========

-------------------------------------------
control and manage cloud computer instances
-------------------------------------------

:Author: openstack@lists.openstack.org
:Date:   2017-01-15
:Copyright: OpenStack Foundation
:Version: 15.0.0
:Manual section: 1
:Manual group: cloud computing

SYNOPSIS
========

  nova-manage <category> <action> [<args>]

DESCRIPTION
===========

nova-manage controls cloud computing instances by managing shell selection, vpn connections, and floating IP address configuration. More information about OpenStack Nova is at http://nova.openstack.org.

OPTIONS
=======

The standard pattern for executing a nova-manage command is:
``nova-manage <category> <command> [<args>]``

Run without arguments to see a list of available command categories:
``nova-manage``

You can also run with a category argument such as user to see a list of all commands in that category:
``nova-manage db``

These sections describe the available categories and arguments for nova-manage.

Nova Database
~~~~~~~~~~~~~

``nova-manage db version``

    Print the current main database version.

``nova-manage db sync``

    Sync the main database up to the most recent version. This is the standard way to create the db as well.

``nova-manage db archive_deleted_rows [--max_rows <number>] [--verbose]``

    Move deleted rows from production tables to shadow tables. Specifying
    --verbose will print the results of the archive operation for any tables
    that were changed.

``nova-manage db null_instance_uuid_scan [--delete]``

    Lists and optionally deletes database records where instance_uuid is NULL.

Nova API Database
~~~~~~~~~~~~~~~~~

``nova-manage api_db version``

    Print the current cells api database version.

``nova-manage api_db sync``

    Sync the api cells database up to the most recent version. This is the standard way to create the db as well.

Nova Cells v2
~~~~~~~~~~~~~

``nova-manage cell_v2 simple_cell_setup [--transport-url <transport_url>]``

    Setup a fresh cells v2 environment; this should not be used if you
    currently have a cells v1 environment. Returns 0 if setup is completed
    (or has already been done), 1 if no hosts are reporting (and cannot be
    mapped), 1 if no transport url is provided for the cell message queue,
    and 2 if run in a cells v1 environment.

``nova-manage cell_v2 map_cell0 [--database_connection <database_connection>]``

    Create a cell mapping to the database connection and message queue
    transport url for the cell0 database. The cell0 database is used for
    instances that have not been scheduled to any cell. This generally
    applies to instances that have encountered an error before they have been
    scheduled. Returns 0 if cell0 is created successfully or already setup.

``nova-manage cell_v2 map_instances --cell_uuid <cell_uuid> [--max-count <max_count>]``

    Map instances to the provided cell. Instances in the nova database will
    be queried from oldest to newest and mapped to the provided cell. A
    max_count can be set on the number of instance to map in a single run.
    Repeated runs of the command will start from where the last run finished
    so it is not necessary to increase max-count to finish. Returns 0 if all
    instances have been mapped, and 1 if there are still instances to be
    mapped.

Nova Logs
~~~~~~~~~

``nova-manage logs errors``

    Displays nova errors from log files.

``nova-manage logs syslog <number>``

    Displays nova alerts from syslog.

Nova Shell
~~~~~~~~~~

``nova-manage shell bpython``

    Starts a new bpython shell.

``nova-manage shell ipython``

    Starts a new ipython shell.

``nova-manage shell python``

    Starts a new python shell.

``nova-manage shell run``

    Starts a new shell using python.

``nova-manage shell script <path/scriptname>``

    Runs the named script from the specified path with flags set.

Nova Project
~~~~~~~~~~~~

``nova-manage project quota <project_id> [--user <user_id>] [--key <key>] [--value <value>]``

    Create, update or display quotas for project/user.  If a key is
    not specified then the current usages are displayed.

``nova-manage project quota_usage_refresh <project_id> [--user <user_id>] [--key <key>]``

    Refresh the quota usages for the project/user so that the
    usage record matches the actual used.  If a key is not specified
    then all quota usages relevant to the project/user are refreshed.

SEE ALSO
========

* `OpenStack Nova <http://nova.openstack.org>`__

BUGS
====

* Nova bugs are managed at Launchpad `Bugs : Nova <https://bugs.launchpad.net/nova>`__



