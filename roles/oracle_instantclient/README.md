oracle_instantclient
====================

Role for installing Oracle instantclient on a Linux system from zip files.

Services defined in the `oracle_services` variable will be templated into `tnsnames.ora` on the destination system.

See [defaults/main.yml](defaults/main.yml) for configuration options, including the location of the instantclient zip files and the version to install

`ansible-playbook ... --extra-vars "instantclient_zips=/path/to/instantclient_zips"`
