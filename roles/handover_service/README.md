# handover_service

Ansible role for deploying [DukeDSHandoverService](https://github.com/Duke-GCB/DukeDSHandoverService/)

This role installs two named docker containers (web and db) to run the DukeDSHandoverService application.

# Usage

This role reads the following variables out of a **handover_service** dictionary. Since some values are secret, this data should not be stored in plaintext.

    handover_service:
      network: handover
      env:
        HANDOVERSERVICE_SECRET_KEY: 'randomly-generated-key-here'
        HANDOVERSERVICE_DDSCLIENT_URL: 'https://dataservice.hostname/api/v1'
        HANDOVERSERVICE_DDSCLIENT_PORTAL_ROOT: 'https://dataservice.hostname'
        HANDOVERSERVICE_DDSCLIENT_AGENT_KEY: 'agent-key-here'
        HANDOVERSERVICE_SMTP_HOST: 'smtp-host'
        HANDOVERSERVICE_ROOT: 'https://deployment.hostname'
        POSTGRES_USER: 'handover_user'
        POSTGRES_PASSWORD: 'generated-posgres-password-here'
        POSTGRES_DB: 'handover'
