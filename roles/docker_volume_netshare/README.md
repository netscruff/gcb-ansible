# docker_volume_netshare

Ansible role to install and configure [docker-volume-netshare](https://github.com/gondor/docker-volume-netshare) volume plugin

# Requirements

1. A debian-based system. The role uses `apt` to install the docker-volume-netshare plugin and the CIFS/NFS utilities
2. Docker 1.9 or later

# Usage

This role installs the service on a server, so that a user can create and use docker volumes that are actually CIFS or NFS mounts.

## Running Ansible

1. Provide variable values for mode and credentials. See [defaults/main.yml](defaults/main.yml) for defaults examples. How you provide these will depend on your ansible configuration, but a good place to start is in an encrypted `host_vars/host` or `group_vars/group` file - see [Ansible Playbooks Best Practices](http://docs.ansible.com/ansible/playbooks_best_practices.html#directory-layout) for more information.
2. Run a playbook including the role (must be `sudo` or `become` since role installs packages and configures services

        $ ansible-playbook -i inventory docker-volumes.yml

## Creating docker volumes

Once the service has been installed, it will respond to `docker volume` commands that use the `cifs` driver.

1. Create a docker volume on the docker host. The name specifies the host and share path. It's just the CIFS or SMB url without the `smb://` or `cifs://`

        $ sudo docker volume create -d cifs --name host.example.com/share
        host.example.com/share

2. A docker volume exists, but the host has not yet tried to mount it.

        $ sudo docker volume ls
        DRIVER              VOLUME NAME
        cifs                host.example.com/share
        
3. To attach the volume to a container, use its name as the source volume

        $ sudo docker run -v host.example.com/share:/cifs_volume -it ubuntu bash
        root@b9c198a5ce5b:/# echo "Hello from Docker!"  > /cifs_volume/hello.txt

# Notes / Caveats

Tested with CIFS only. Places CIFS mount credentials in /.netrc on the host. So you should assume that users with docker access on the host can read your credentials file.

Characters in the password that would need to be escaped on the command-line (e.g. `$` or `%` do need to be escaped in the .netrc file. [GitHub issue](https://github.com/gondor/docker-volume-netshare/issues/18). To achieve the correct amount of escaping, characters in an ansible vars file should be escaped with two backslashes: `$` becomes `\\$` and `%` becomes `\\%`.

When docker-volume-netshare mounts a CIFS volume, the files will likely owned by root (uid 0). This ownership and permission cascades into the docker container, so if your docker container runs as a non-root user, it may be unable to write to the volume.

The docker-volume-netshare plugin documentation indicates that credentials could be provided at time of volume creation, but we have not had success here. This would be preferrable for recommending to users.

The .netrc file is only read by docker-volume-netshare when the service starts. If you make changes to this file, you must restart the `docker-volume-netshare` service.
