# ansible-playbook-pssid-gui

Ansible playbook for deploying [pSSID-GUI](https://github.com/UMNET-perfSONAR/pSSID-GUI) to a server. It installs Docker, pSSID-GUI, Ansible, and [ansible-playbook-pssid-daemon](https://github.com/UMNET-perfSONAR/ansible-playbook-pssid-daemon).

## Clone this playbook

```
git clone https://github.com/UMNET-perfSONAR/ansible-playbook-pssid-gui.git
cd ansible-playbook-pssid-gui
```



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
ansible-playbook \
  playbook.yml \
  -i IP_ADDR, 
```

Change `IP_ADDR` to the IP address of the intended target, but take note of the trailing comma.

If everything was successful, opening that IP address at the port specified in `playbook.yml` should return the pSSID GUI.

## Runtime Configuration

To modify settings such as the location of `default-inventory`, the directory inventories are stored in, or the port of the web app at runtime, modify `/etc/pssid-gui/config` on the target machine. Then navigate to the directory containing pSSID-GUI and run `docker-compose --env-file /etc/pssid-gui/config up -d` to restart it.

To use the generated inventories to push configs to probes, `cd` into the `ansible-playbook-pssid-daemon` directory (adjacent to the pSSID-GUI directory, default `/usr/local/ansible-playbook-pssid-daemon`) and run the following: 

```
ansible-playbook playbooks/push-configs.yml -i /var/lib/pssid-gui/inventories/inv-name/inventory --ask-become-pass
```
