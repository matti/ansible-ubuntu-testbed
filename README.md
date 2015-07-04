# ansible-testing

## install
	brew install ansible

	echo "\n" | sudo tee -a /etc/hosts
	echo "127.0.0.1\ttestbed-proxy" | sudo tee -a /etc/hosts
	echo "127.0.0.1\ttestbed-app" | sudo tee -a /etc/hosts

	echo "[proxyservers]" > hosts
	echo "testbed-proxy         ansible_ssh_port=2200        ansible_ssh_user=vagrant        ansible_ssh_private_key_file=$(pwd)/.vagrant/machines/proxy/virtualbox/private_key" >> hosts

	echo "\n[appservers]" >> hosts
	echo "testbed-app         ansible_ssh_port=2210        ansible_ssh_user=vagrant        ansible_ssh_private_key_file=$(pwd)/.vagrant/machines/app/virtualbox/private_key" >> hosts

## reinstall

	vagrant halt
	vagrant destroy -f

## setup

	source env
	vagrant up

## testing
	ansible all -i hosts -m ping
	ansible proxyservers -i hosts -m ping

## site playbook

### install requirements

	# rm -rf roles first..
	ansible-galaxy install -r requirements.yml

	# ..or ignore errors
	ansible-galaxy install -r requirements.yml --ignore-errors

### play

	ansible-playbook site.yml -i hosts
