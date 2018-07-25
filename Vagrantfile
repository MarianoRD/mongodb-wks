Vagrant.configure('2') do |config|
  config.vm.box = 'bento/ubuntu-16.04'
  config.vm.network 'public_network',
                    bridge: 'wlp4s0',
                    auto_config: true,
                    use_dhcp_assigned_default_route: true

  config.vm.provider :virtualbox do |vb|
    vb.customize ['modifyvm', :id, '--natdnshostresolver1', 'on']
    vb.customize ['modifyvm', :id, '--memory', 3072]
    vb.customize ['modifyvm', :id, '--name', 'mongodb']
    vb.customize ['modifyvm', :id, '--cpus', '1']
  end

  config.vm.provision 'shell', inline: <<-SHELL
    useradd ubuntu
    mkdir -p /home/ubuntu/.ssh
    chown -R ubuntu:ubuntu /home/ubuntu
  SHELL

  config.vm.provision :ansible_local do |ansible|
    ansible.playbook  = 'ansible/provision.yml'
    ansible.verbose   = true
    ansible.install   = true
    ansible.limit     = 'all'
  end

end
