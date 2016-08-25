[![Build Status](https://travis-ci.org/CSC-IT-Center-for-Science/ansible-role-collectd.svg)](https://travis-ci.org/CSC-IT-Center-for-Science/ansible-role-collectd)
ansible-role-collectd
=========

Configures a collectd with a few roles

Requirements
------------

/etc/collectd.d/ directory

Role Variables
--------------

Example for how to add more plugins and how to configure them when using the apache encoder style.

Want to configure collectd to ship metrics with the collectd protocol with a username/password and set graphite prefix? Set this:

<pre>
collectd_tsdb_writer: False
collectd_network_server: True
collectd_set_graphite_prefix: True
collectd_graphite_prefix_1: "^service\\.clustername\\."
collectd_graphite_prefix_2: "service.clustername."

collectd_plugins_processes: ""
collectd_plugins_network:
  - options:
    - LoadPlugin: network
  - sections:
    - name: Plugin
      param: network
      content:
        - options:
          - Forward: True
        - sections:
          - name: Server
            param: "{{ collectd_network_server_host }}"
            content:
              - options:
                - SecurityLevel: Encrypt
                - Username: "{{ collectd_username }}"
                - Password: "{{ collectd_password }}"
#
collectd_plugins_custom: "{{
  collectd_plugins_aggregation +
  collectd_plugins_cpufreq +
  collectd_plugins_exec +
  collectd_plugins_network
}}"

</pre>

External IPMI scripts

This role fetches a few scripts from other github repos for IPMI statistics.
If you set "collectd_force_geturl: True" then this role will re-download those scripts if they already exists. 

With collectd_drop_rsyslog_spam True we install an rsyslog.d/ file that drops "value has been dispatche
d" syslog messages from the exec plugin.

Dependencies
------------

Some ideas borrowed from https://github.com/picotrading/ansible-collectd and that role uses the apache\_encoder\_macro.j2 from picotrading - 

<pre>
https://raw.githubusercontent.com/picotrading/config-encoder-macros/master/macros/apache_encode_macro.j2
</pre>

ansible 2.0 (because checksum= with get_url: module)

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
