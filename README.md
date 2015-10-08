ansible-role-collectd
=========

Configures a collectd with a few roles

Requirements
------------

/etc/collectd.d/ directory

Role Variables
--------------


Dependencies
------------

Some ideas borrowed from https://github.com/picotrading/ansible-collectd and that role uses the apache\_encoder\_macro.j2 from picotrading - 

<pre>
https://raw.githubusercontent.com/picotrading/config-encoder-macros/master/macros/apache_encode_macro.j2
</pre>

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: ansible-role-collectd }

License
-------

MIT

Author Information
------------------
