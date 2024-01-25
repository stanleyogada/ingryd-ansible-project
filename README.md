# INGRYD-ANSIBLE-PROJECT
# Ansible Project: Server Configuration Management

## Overview

This Ansible project is designed to automate the configuration and management of servers running Oracle Linux and Ubuntu. It includes roles and plays for updating local repositories, performing system updates, and configuring different types of servers such as web servers, database servers, and file servers.

## Project Structure

- `roles/`
  - `base/`: Role for updating the public key of the `oga` user.
  - `web_servers/`: Role for configuring web servers.
  - `db_servers/`: Role for configuring database servers.
  - `file_servers/`: Role for configuring file servers.

- `sys_config.yml`: Main Ansible playbook containing plays for updating repositories, updating all servers, and configuring specific server types.

## Prerequisites for One-Time Success Run

Before running the playbooks, ensure the following prerequisites are met:

1. **User Setup:**
   - Create a user named `zero` on all target servers with sudo access.
   - Ensure that the password for the `zero` user is the same across all servers.

2. **SSH Public Key Authentication:**
   - Set up SSH public key authentication from the control host to each server for the `zero` user.
   - Make sure that the control host can SSH into each server without entering a password.

3. **Ad-Hoc Command Password:**
   - When using Ansible ad-hoc commands, provide the `--ask-become` or `-K` option to enter the sudo password for the `zero` user.
   ```bash
   ansible-playbook bootstrap.yml ays_config.yml -K
   ```
   - Run the above ad-hoc once hence the name bootstrap
   - After a successful run you may remove the `-K` as the user called `oga` is now the active remote user and doesn’t require password to use sudo

## Usage

1. Ensure Ansible is installed on the control machine.
   ```bash
   apt install ansible
   ```

2. Clone the repository.
   ```bash
   git clone https://github.com/stanleyogada/ingryd-ansible-project/.git
   cd ingryd-ansible-project
   ```

3. Edit the inventory file (`inventory.ini`) to specify your target servers and their groups (web_servers, db_servers, file_servers).

4. Review and customize the variables in the roles based on your server configurations.

5. Run the playbook.
   ```bash
   ansible-playbook sys_config.yml
   ```

## Plays and Roles

### Update Local Repositories

- **Description:** This play updates the local repositories for Oracle Linux and Ubuntu servers.

### Update All Servers

- **Description:** This play installs updates for all servers.

### Configure Web Servers

- **Description:** This play configures servers designated as web servers using the `web_servers` role.

### Configure Database Servers

- **Description:** This play configures servers designated as database servers using the `db_servers` role.

### Configure File Servers

- **Description:** This play configures servers designated as file servers using the `file_servers` role.

## Tags

- `update`: Used for plays related to updating servers.
- `oracleLinux`: Used for tasks specific to Oracle Linux.
- `ubuntu`: Used for tasks specific to Ubuntu.

## Notes

- Ensure you have the necessary permissions to perform system updates and configurations on the target servers.
- Monitor the playbook execution for any errors or warnings.
- Customize variables and configurations in roles based on your specific requirements.

Feel free to contribute to this Ansible project or raise issues if you encounter any problems. Happy automating!
