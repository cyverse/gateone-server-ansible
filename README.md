# gateone-server-ansible
This repo provides the ansible playbook and role needed to install gateone.  To use this with your ansible, you should link role into the roles directory.  By default, the roles directory is /etc/ansible/roles. You'll also need to define a few variables. Currently, this playbook and role assumes Ubuntu. With a little effort, other distros could be supported.

## Installation

1. git clone gateone-server-ansible repo (e.g. into /opt/gateone-server-ansible)
2. Assuming roles is in /etc/ansible/roles, ln -s /opt/gateone-server-ansbile/ /etc/ansible/roles/
3. Define the host(s) into /etc/ansible/hosts (or wherever your hosts file is configured for).  The playbook assumes the server(s) are defined in the host group called "gateone-servers".
4. Define the following variables, generally in the hosts file or group_vars:
* GATEONE_REPO: location of the gateone repo
* GATEONE_CONFIG_REPO: location of the config repo
* SSH_HOST_SRC: directory containing ssl certs
* SSH_HOST_KEY: ssl key file name
* SSH_HOST_CERT: ssl cert file name
* UFW_DO_CONFIGURE: boolean whether to configure ufw or not
* UFW_INCOMING_ALLOW: array of dictionary items containing ip and ports to allow incoming (each array element has an ip and port to allow incoming). UFW is executed only if UFW_DO_CONFIGURE is true
* UFW_OUTGOING_ALLOW: array of dictionary items containing ip and ports to allow outgoing, similar to UFW_INCOMING_ALLOW. UFW is executed only if UFW_DO_CONFIGURE is true.
5. the gateone server should start after the playbook is executed, assuming the configuration is correct

## Other notes

* Simple inventory files are located in the inventory_samples directory

* The GATEONE_CONFIG_REPO assumes the following files exist:
** 10server.conf
** 20authentication.conf
** 50terminal.conf
** ssh_config_global
