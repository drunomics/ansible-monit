Role Name
=========

Installs monit https://mmonit.com/monit/ for monitoring of processes and services. Configuration ready with some defaults.

Requirements
------------

None.

Role Variables
--------------

````
---
# defaults file for ansible-monit
config_monit: false  #defines if monit should be configured after installed
monit_email_from: monit@$HOST
monit_email_to: root@localhost
monit_email_server: localhost
monit_enable_email_notifications: false  #defines if monit email notifications are to be sent.
monit_enable_web_server: false  #defines if monit web server is enabled.
monit_monitor_services:
  - name: apache2
    cpu_checks:
      - name: cpu
        percentage: 40%
        cycles: 2
        action: alert
      - name: totalcpu
        percentage: 60%
        cycles: 2
        action: alert
      - name: totalcpu
        percentage: 80%
        cycles: 5
        action: restart
    failed_host: 127.0.0.1
    failed_host_port: 80
    monitored: true
    pidfile: /var/run/apache2/apache2.pid
    start_program: /usr/sbin/service apache2 start
    stop_program: /usr/sbin/service apache2 stop
  - name: mysql
    failed_host: 127.0.0.1
    failed_host_port: 3306
    monitored: true
    pidfile: /var/run/mysqld/mysqld.pid
    start_program: /usr/sbin/service mysql start
    stop_program: /usr/sbin/service mysql stop
  - name: rsyslogd
    monitored: true
    pidfile: /var/run/rsyslogd.pid
    start_program: /usr/sbin/service rsyslog start
    stop_program: /usr/sbin/service rsyslog stop
  - name: sshd
    failed_host: 127.0.0.1
    failed_host_port: 22
    monitored: true
    pidfile: /var/run/sshd.pid
    start_program: /usr/sbin/service ssh start
    stop_program: /usr/sbin/service ssh stop
monit_web_server_allow_list:
  - 10.0.0.0/8
  - 172.16.0.0/16
  - 192.168.0.0/16
  - localhost
monit_web_server_local_only: true  #defines if web server gui is allowed from only the localhost otherwise defined web_server_allow_list above.
monit_web_server_password: monit
monit_web_server_username: admin
````

Dependencies
------------

None.

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: mrlesmithjr.monit }

License
-------

BSD

Author Information
------------------

Larry Smith Jr.
- @mrlesmithjr
- http://everythingshouldbevirtual.com
- mrlesmithjr [at] gmail.com
