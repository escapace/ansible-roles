Vagrant.require_version ">= 2.0.0"

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"

  # Disable the new default behavior introduced in Vagrant 1.7, to
  # ensure that all Vagrant machines will use the same SSH key pair.
  # See https://github.com/mitchellh/vagrant/issues/5005
  # config.ssh.insert_key = false

  # config.vm.provision "ansible" do |ansible|
  #   ansible.verbose = "v"
  #   ansible.playbook = "playbook.yml"
  # end
  config.vm.synced_folder '.', '/vagrant', disabled: true
  config.vm.provision :shell, :inline => "mkdir -p /home/vagrant/.ssh && chmod 700 /home/vagrant/.ssh"
  config.vm.provision :shell, :inline => "curl https://github.com/epiloque.keys >> /home/vagrant/.ssh/authorized_keys"
  config.vm.provision :shell, :inline => "chown vagrant:vagrant -R /home/vagrant/.ssh && chmod 600 /home/vagrant/.ssh/authorized_keys"
end
