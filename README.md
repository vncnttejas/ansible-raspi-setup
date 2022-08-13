# Raspberry Pi Ansible setup

## Background
- This `ansible-playbook` is written for low end hardware Raspberry Pis, like Raspberry Pi 3 or below
- The playbook makes use of community contributed roles
- The playbook does the following tasks
  - Mount HDD of a given uuid
  - Installs and sets up a `ufw` firewall with allow access to `192.168.0.*` ips, with following open ports
    - 22 (ssh)
    - 9091 (transmission)
  - Installs `transmission` deaemon and sets the download path to `<hdd>/.tor` folder for incomplete files and `<hdd>/QuickDump` folder for completed files

## Setup
- Install python dependencies from pyproject.yaml file via poetry 
  (optional, if you already have these installed)
  ```shell
  $ poetry install
  ```

- If you ran the first step then run the following command to set the poetry shell, otherwise you won't find `ansible` packages (unless they're installed globally)
  ```shell
  $ poetry shell
  ```

- Install ansible *requirements* (ansible-roles) with the following command
  ```shell
  $ ansible-galaxy install -r requirements.yml --roles-path roles
  ```

- Copy the sample vars file and create the `vars.yml` file from it
  ```shell
  $ cp vars.yml.example vars.yml
  ```

- Update the variables as needed
  - to get `hdd_uuid`, run the commands `lsblk` and `blkid`

- Run the ansible playbook
  ```shell
  $ ansible-playbook main.yml -v -i inventory.txt -u <remote-username>
  ```

- Reboot the pi and start using it with all the above packages