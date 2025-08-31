# K3s Deployment with Ansible

This repository provides a simple setup for deploying K3s using an Ansible playbook. The script ensures that Ansible is installed on your system if it's not already present, and then runs the specified playbook to deploy K3s.

## Prerequisites

- Python 3.x
- `pip` or another package manager (e.g., `apt`, `yum`)
- A text editor for modifying files

## Setup Instructions

1. **Clone the Repository**
   Clone this repository onto your local machine:
   ```sh
   git clone https://github.com/yourusername/k3s-deployment.git
   cd k3s-deployment

2. Prepare Inventory File Ensure that you have an inventory.ini file in the root directory of the project with the necessary host definitions for your Ansible playbook.

3. Install Dependencies (Optional) If you don't already have Python and pip installed, install them using your system's package manager:

```sh
sudo apt-get update && sudo apt-get install python3-pip
```

4. **Use the Makefile**

Open a terminal in the cloned repository directory.
Run the following command to ensure that Ansible is installed and then run the playbook:

```sh
make all
```

The all target in the Makefile performs the following steps:

- Checks if Ansible is already installed on your system.
- If not, it installs Ansible using pip.
- Runs the Ansible playbook specified by ansible-playbook -i inventory.ini k3s.yml.


## Directory Structure

- Makefile: Contains rules for checking and installing Ansible and running the playbook.
- inventory.ini: Contains configuration details about your hosts, variables, etc.

## Customization

You can customize the Makefile to run different commands or adjust paths as needed. For example:

Change the path where `.installed_ansible` file is created if you prefer a different location.
Adjust the installation command for Ansible if you use a different package manager (e.g., `sudo apt-get install ansible`).
