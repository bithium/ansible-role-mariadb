MariaDB
=======

This role installs [MariaDB](https://mariadb.org/) into your system.

Requirements
------------

No special requirements; note that this role requires root access, so either run it in a playbook
with a global `become: yes`, or invoke the role in your playbook like:

    - hosts: database
      roles:
        - role: bithium.mariadb
          become: yes

Please also be advised that this role runs the script `/usr/bin/mysql_secure_installation` in order to
secure the installation, setting the root database user to `mariadb_root_password` and answering `Y` to
all other questions.

Role Variables
--------------

Available variables are listed below, along with default values (see `defaults/main.yml` and `vars/main.yml`):

 * Packages to install:

   ```yaml
   mariadb_packages:
   - mariadb
   - mysql-client
   ```

 * Database service name:

   ```yaml
   mariadb_service: mariadb
   ```

 * Configuration folder:

   ```yaml
   mariadb_config_dir: /etc/mysql
   ```

 * Main configuration file:

   ```yaml
   mariadb_config_file: "{{mariadb_config_dir}}/my.cnf"
   ```

 * Extra configuration folder:

   ```yaml
   mariadb_extra_config_dir: /etc/mysql/conf.d
   ```

 * Extra configuration file:

   ```yaml
   mariadb_extra_config_file: "{{mariadb_extra_config_dir}}/25_ansible.cnf"
   ```

 * Database configuration:

   ```yaml
   mariadb_config: {}
   ```

   For example the following `mariadb_config` definition:

   ```yaml
   mariadb_config:
     mysqld:
       - skip-networking
       - table_open_cache: 128
     mysql:
       - safe-updates
   ```

   Will generate the following configuration file:

   ```ini
   [mysql]
   skip-networking
   table_open_cache = 128

   [mysql]
   safe-updates
   ```

  * Root user database password: `mariadb_root_password`
    **WARNING**: This variable has no default value and **MUST** be defined by the user of the role.

Dependencies
------------

This role has no external roles dependencies.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables
passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: mariadb, x: 42 }

License
-------

Apache 2.0

Author Information
------------------

[Bithium S.A.](http://www.bithium.com)
