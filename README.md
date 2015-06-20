# ansible-testing

## init
	vagrant up

	echo "127.0.0.1\tlocalbuntu" | sudo tee -a /etc/hosts
	echo "localbuntu         ansible_ssh_port=2222        ansible_ssh_user=vagrant        ansible_ssh_private_key_file=$(pwd)/.vagrant/machines/default/virtualbox/private_key" > ansible_hosts

## setup

	vagrant up
	source env

## testing

	ansible all -i ansible_hosts -m ping
