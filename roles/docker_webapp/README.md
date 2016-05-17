# docker_webapp

Ansible role for common web application configuration with docker

This role places SSL keys/certificates on a host for web servers and shibboleth SPs. It also creates a docker bridge network, allowing multiple containers to connect to each other by container name.

# Usage

This role reads the following variables out of a **docker_webapp** dictionary. Since SSL keys are private, this data should not be stored in plaintext. Values not required can be safely omitted.

    docker_webapp:
       ssl_dir: # Base directory on host to contain SSL certificates and keys
       ssl_cert: # Web server certificate text
       ssl_cert_file: # Name of file to populate with certificate text
       ssl_key: # Web server private key text
       ssl_key_file: # Name of file to populate with private key text
       shib_dir: # Base directory on host to contain Shibboleth certificates and keys
       shib_sb_cert: # Shibboleth SP certificate text
       shib_sb_cert_file: # Name of file to populate with certificate text
       shib_sb_key: # Shibboleth SP private key text
       shib_sb_key_file: # Name of file to populate with private key text
       network: # Name of docker bridge network to create if not present
