
    Use a Linux account with login capability
        Make sure the account has the same UID/GID on all cluster nodes

[ec2-user@ip-172-31-21-228 ~]$ sudo cat /etc/passwd | grep ferdinand
ferdinand:x:1200:502::/home/ferdinand:/bin/bash


[ec2-user@ip-172-31-21-231 ~]$ export HUE_CONF_DIR="/var/run/cloudera-scm-agent/process/`sudo ls -alrt /var/run/cloudera-scm-agent/process | grep HUE | tail -1 | awk '{print $9}'`"


[ec2-user@ip-172-31-21-231 ~]$ sudo /opt/cloudera/parcels/CDH/lib/hue/build/env/bin/hue useradmin_sync_with_unix --min-uid 1200 --max-uid 1200

Traceback (most recent call last):
  File "/opt/cloudera/parcels/CDH/lib/hue/build/env/bin/hue", line 12, in <module>
    load_entry_point('desktop==3.9.0', 'console_scripts', 'hue')()
  File "/opt/cloudera/parcels/CDH-5.8.2-1.cdh5.8.2.p0.3/lib/hue/desktop/core/src/desktop/manage_entry.py", line 59, in entry
    execute_from_command_line(sys.argv)
  File "/opt/cloudera/parcels/CDH-5.8.2-1.cdh5.8.2.p0.3/lib/hue/build/env/lib/python2.6/site-packages/Django-1.6.10-py2.6.egg/django/core/management/__init__.py", line 399, in execute_from_command_line
    utility.execute()
  File "/opt/cloudera/parcels/CDH-5.8.2-1.cdh5.8.2.p0.3/lib/hue/build/env/lib/python2.6/site-packages/Django-1.6.10-py2.6.egg/django/core/management/__init__.py", line 392, in execute
    self.fetch_command(subcommand).run_from_argv(self.argv)
  File "/opt/cloudera/parcels/CDH-5.8.2-1.cdh5.8.2.p0.3/lib/hue/build/env/lib/python2.6/site-packages/Django-1.6.10-py2.6.egg/django/core/management/base.py", line 242, in run_from_argv
    self.execute(*args, **options.__dict__)
  File "/opt/cloudera/parcels/CDH-5.8.2-1.cdh5.8.2.p0.3/lib/hue/build/env/lib/python2.6/site-packages/Django-1.6.10-py2.6.egg/django/core/management/base.py", line 285, in execute
    output = self.handle(*args, **options)
  File "/opt/cloudera/parcels/CDH-5.8.2-1.cdh5.8.2.p0.3/lib/hue/apps/useradmin/src/useradmin/management/commands/useradmin_sync_with_unix.py", line 47, in handle
    sync_unix_users_and_groups(min_uid, max_uid, min_gid, max_gid, check_shell)
  File "/opt/cloudera/parcels/CDH-5.8.2-1.cdh5.8.2.p0.3/lib/hue/apps/useradmin/src/useradmin/views.py", line 683, in sync_unix_users_and_groups
    hue_group = Group.objects.get(name=name)
  File "/opt/cloudera/parcels/CDH-5.8.2-1.cdh5.8.2.p0.3/lib/hue/build/env/lib/python2.6/site-packages/Django-1.6.10-py2.6.egg/django/db/models/manager.py", line 151, in get
    return self.get_queryset().get(*args, **kwargs)
  File "/opt/cloudera/parcels/CDH-5.8.2-1.cdh5.8.2.p0.3/lib/hue/build/env/lib/python2.6/site-packages/Django-1.6.10-py2.6.egg/django/db/models/query.py", line 304, in get
    num = len(clone)
  File "/opt/cloudera/parcels/CDH-5.8.2-1.cdh5.8.2.p0.3/lib/hue/build/env/lib/python2.6/site-packages/Django-1.6.10-py2.6.egg/django/db/models/query.py", line 77, in __len__
    self._fetch_all()
  File "/opt/cloudera/parcels/CDH-5.8.2-1.cdh5.8.2.p0.3/lib/hue/build/env/lib/python2.6/site-packages/Django-1.6.10-py2.6.egg/django/db/models/query.py", line 857, in _fetch_all
    self._result_cache = list(self.iterator())
  File "/opt/cloudera/parcels/CDH-5.8.2-1.cdh5.8.2.p0.3/lib/hue/build/env/lib/python2.6/site-packages/Django-1.6.10-py2.6.egg/django/db/models/query.py", line 220, in iterator
    for row in compiler.results_iter():
  File "/opt/cloudera/parcels/CDH-5.8.2-1.cdh5.8.2.p0.3/lib/hue/build/env/lib/python2.6/site-packages/Django-1.6.10-py2.6.egg/django/db/models/sql/compiler.py", line 713, in results_iter
    for rows in self.execute_sql(MULTI):
  File "/opt/cloudera/parcels/CDH-5.8.2-1.cdh5.8.2.p0.3/lib/hue/build/env/lib/python2.6/site-packages/Django-1.6.10-py2.6.egg/django/db/models/sql/compiler.py", line 785, in execute_sql
    cursor = self.connection.cursor()
  File "/opt/cloudera/parcels/CDH-5.8.2-1.cdh5.8.2.p0.3/lib/hue/build/env/lib/python2.6/site-packages/Django-1.6.10-py2.6.egg/django/db/backends/__init__.py", line 162, in cursor
    cursor = util.CursorWrapper(self._cursor(), self)
  File "/opt/cloudera/parcels/CDH-5.8.2-1.cdh5.8.2.p0.3/lib/hue/build/env/lib/python2.6/site-packages/Django-1.6.10-py2.6.egg/django/db/backends/__init__.py", line 132, in _cursor
    self.ensure_connection()
  File "/opt/cloudera/parcels/CDH-5.8.2-1.cdh5.8.2.p0.3/lib/hue/build/env/lib/python2.6/site-packages/Django-1.6.10-py2.6.egg/django/db/backends/__init__.py", line 127, in ensure_connection
    self.connect()
  File "/opt/cloudera/parcels/CDH-5.8.2-1.cdh5.8.2.p0.3/lib/hue/build/env/lib/python2.6/site-packages/Django-1.6.10-py2.6.egg/django/db/utils.py", line 99, in __exit__
    six.reraise(dj_exc_type, dj_exc_value, traceback)
  File "/opt/cloudera/parcels/CDH-5.8.2-1.cdh5.8.2.p0.3/lib/hue/build/env/lib/python2.6/site-packages/Django-1.6.10-py2.6.egg/django/db/backends/__init__.py", line 127, in ensure_connection
    self.connect()
  File "/opt/cloudera/parcels/CDH-5.8.2-1.cdh5.8.2.p0.3/lib/hue/build/env/lib/python2.6/site-packages/Django-1.6.10-py2.6.egg/django/db/backends/__init__.py", line 115, in connect
    self.connection = self.get_new_connection(conn_params)
  File "/opt/cloudera/parcels/CDH-5.8.2-1.cdh5.8.2.p0.3/lib/hue/build/env/lib/python2.6/site-packages/Django-1.6.10-py2.6.egg/django/db/backends/sqlite3/base.py", line 347, in get_new_connection
    conn = Database.connect(**conn_params)
django.db.utils.OperationalError: unable to open database file

    Get a screenshot that shows this user is logged into Hue
        Name the file client/labs/0_unix_login.png

