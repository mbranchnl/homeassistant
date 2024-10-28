# Home Assistant

This role will install Home Assistant based on the [supervised installer](https://github.com/home-assistant/supervised-installer) this role will follow all mandatory steps as required in the [requirements](https://github.com/home-assistant/architecture/blob/master/adr/0014-home-assistant-supervised.md) setup by Home Assistant.

Why this role? First of all it's fun to build, and i wanted more controle over the docker images i want to run in this environment. For instance i can manage my own images through ansible that are supportive to Home Assistant. For instance i will have more control over my PostgreSQL recorder or i can install/configure my pihole besides it.

This README.md will contain all manual steps, and other need to knows during the build of this role. This role also includes some personal preferences of the author and has some initials steps that are already done as described in the prerequisites

## Prerequisites

Packages needed to be installated on the server in order to execute this role are;

Install sudo manually in order to allow the example inventory:

```bash
apt install sudo
```

Create sudoers-file:

```bash
echo "username ALL=(ALL:ALL) ALL" | sudo tee /etc/sudoers.d/username
```

The server is configured with a static IP based on the default advised network configuration of the installer, the configuration can be found in, example;

```bash
/etc/network/interfaces.d/ens18
```

### Inventory

This is an example inventory:

```yaml
all:
  hosts:
    homeassistant:
      ansible_host: x.x.x.x
      ansible_user: username
      ansible_password: password
      ansible_become_password: "{{ ansible_password }}"
      ansible_become_user: "root"
```

### Playbook

This is an example playbook:

```yaml
---
- hosts: homeassistant
  gather_facts: true
  become: true
  roles:
    - homeassistant
```
