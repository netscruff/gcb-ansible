# d4s2_webapp

Ansible role for deploying [D4S2](https://github.com/Duke-GCB/d4s2/)

This role installs two named docker containers (web and db) to run the D4s2 application.

## Dependencies

This role depends on the [docker_webapp](../docker_webapp) role.

## Usage

This role reads the following variables out of a **d4s2_config** dictionary. Since some values are secret, this data should not be stored in plaintext.

    d4s2_config:
      network: d4s2
      env:
        D4S2_SECRET_KEY: 'randomly-generated-key-here'
        D4S2_DDSCLIENT_URL: 'https://dataservice.hostname/api/v1'
        D4S2_DDSCLIENT_PORTAL_ROOT: 'https://dataservice.hostname'
        D4S2_DDSCLIENT_AGENT_KEY: 'agent-key-here'
        D4S2_SMTP_HOST: 'smtp-host'
        D4S2_ROOT: 'https://deployment.hostname'
        POSTGRES_USER: 'd4s2_user'
        POSTGRES_PASSWORD: 'generated-posgres-password-here'
        POSTGRES_DB: 'd4s2_db'
