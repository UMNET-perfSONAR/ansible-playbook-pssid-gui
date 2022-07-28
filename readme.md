# ansible-playbook-pssid-gui

Ansible playbook for deploying [pSSID-GUI](https://github.com/UMNET-perfSONAR/pSSID-GUI) to a server. It installs Docker, pSSID-GUI, Ansible, and [ansible-playbook-pssid-daemon](https://github.com/UMNET-perfSONAR/ansible-playbook-pssid-daemon).

## Dependencies

Run the following to get dependencies:

```
ansible-galaxy install -r requirements.yml
ansible-galaxy install -r roles/ansible-role-pssid-gui/requirements.yml
```

## Deployment

### Settings

Within `playbook.yml`, `pssid_gui_*` can be changed to modify the installation of pSSID-GUI.

### Running

```
ansible-playbook playbook.yml -i 1.1.1.1,
```

Change `1.1.1.1` to the IP address of the intended target, but take note of the trailing comma.

If everything was successful, opening that IP address at the port specified in `playbook.yml` should return the pSSID GUI.

## Runtime Configuration

To modify settings such as the location of `default-inventory`, the directory inventories are stored in, or the port of the web app at runtime, modify `/etc/pssid-gui/config` on the target machine. Then navigate to the directory containing pSSID-GUI and run `docker-compose --env-file /etc/pssid-gui/config up -d` to restart it.

This playbook installs [`ansible-playbook-pssid-daemon`](https://github.com/UMNET-perfSONAR/ansible-playbook-pssid-daemon) onto the server. Read through that repository's readme to learn how to turn inventories configured with the GUI into pSSID config files.
