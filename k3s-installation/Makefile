ANSIBLE_PLAYBOOK = ansible-playbook -i inventory.ini k3s.yml

.PHONY: check-ansible install-ansible run-playbook clean all

all: run-playbook

check-ansible:
	which ansible > /dev/null 2>&1
ifeq ($${PIPESTATUS[0]}, 1)
	$(error Ansible not found. Please install it before proceeding.)
endif

install-ansible: check-ansible
ifndef ANSIBLE_INSTALLED
	@echo "Installing Ansible..."
	pip3 install ansible --user
	export PATH=$$PATH:$$HOME/.local/bin
endif


run-playbook: install-ansible
	ansible-playbook -i inventory.ini k3s.yml

clean:
	rm -f .installed_ansible

.installed_ansible:
	touch $@

ANSIBLE_INSTALLED := $(wildcard .installed_ansible)

ifeq ($(shell which ansible 2>/dev/null),)
install-ansible: .installed_ansible
else
run-playbook: .installed_ansible
endif

# Dummy target to ensure `make` has something to do
.PHONY: dummy
dummy:
