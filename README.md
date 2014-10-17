Ansible-Vagrant-Example
=======================

This repo contains two folders: vm-ansible and vm-remoteserver.

vm-ansible represents a server that has Ansible installed and will be used to provision the remote server found in vm-remoteserver.

This repo requires Vagrant to be installed.

To setup the remote server vm:

<pre>
cd vm-remoteserver

vagrant up
</pre>

To setup the Ansible vm (this will create the vm and install Ansible via the script/provision):

<pre>
cd ../vm-ansible

vagrant up
</pre>

We want to make sure the Ansible vm can ssh into the remote server vm. So we generate an ssh key in the Ansible vm and add the public part to the remote server vm.

In the Ansible vm run the following script:

<pre>
source ./script/add-rsa-key
</pre>

We also need to tell Ansible which server it has access to, which we do via the inventory file found at /etc/ansible/hosts. Copy the following text to /etc/ansible/hosts:

<pre>
[southwest]
172.16.32.33
</pre>

Now we can run Ansible commands in the Ansible vm i.e. ansible all -m ping. Or you can run one of the playbooks found in the playbooks folder e.g.

<pre>
ansible-playbook playbooks/ping.yml
</pre>
