# ansible-playbook-pssid-gui

Ansible playbook for deploying [pSSID-GUI](https://github.com/UMNET-perfSONAR/pSSID-GUI) to a server. It installs Docker, pSSID-GUI, Ansible, and [ansible-playbook-pssid-daemon](https://github.com/UMNET-perfSONAR/ansible-playbook-pssid-daemon).

## Dependencies

Run the following to get dependencies:

```
ansible-galaxy install -r requirements.yml
ansible-galaxy install -r roles/ansible-role-pssid-gui/requirements.yml
```

## Usage

### Settings

Within `playbook.yml`, `pssid_gui_*` can be changed to modify the installation of pSSID-GUI. Tweak the tasks below to change the installation of ansible-playbook-pssid-daemon.

### Running

```
ansible-playbook playbook.yml -i 1.1.1.1,
```

Change `1.1.1.1` to the IP address of the intended target, but take note of the trailing comma.

If everything was successful, opening that IP address at the port specified in `playbook.yml` should return the pSSID GUI.

This playbook installed [`ansible-playbook-pssid-daemon`](https://github.com/UMNET-perfSONAR/ansible-playbook-pssid-daemon) onto the server (into `/opt` by default). Read through that repository's readme to learn how to turn inventories configured with the GUI into pSSID config files.
