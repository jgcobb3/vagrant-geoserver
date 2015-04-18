# -*- mode: ruby -*-
# vi: set ft=ruby :

# Deserialize Ansible Galaxy installation metadata for a role
def galaxy_install_info(role_name)
  role_path = File.join("ansible", role_name)
  galaxy_install_info = File.join(role_path, "meta", ".galaxy_install_info")

  if (File.directory?(role_path) || File.symlink?(role_path)) && File.exists?(galaxy_install_info)
    YAML.load_file(galaxy_install_info)
  else
    { install_date: "", version: "0.0.0" }
  end
end

# Uses the contents of roles.txt to ensure that ansible-galaxy is run
# if any dependencies are missing
def install_dependent_roles
  ansible_directory = File.join("ansible")
  ansible_roles_txt = File.join(ansible_directory, "roles.txt")

  File.foreach(ansible_roles_txt) do |line|
    role_name, role_version = line.split(",")
    role_path = File.join(ansible_directory, "roles", role_name)
    galaxy_metadata = galaxy_install_info(role_name)

    if galaxy_metadata["version"] != role_version.strip
      unless system("ansible-galaxy install -f -r #{ansible_roles_txt} -p #{File.dirname(role_path)}")
        $stderr.puts "\nERROR: An attempt to install Ansible role dependencies failed."
        exit(1)
      end

      break
    end
  end
end

# Install missing role dependencies based on the contents of roles.txt
if [ "up", "provision", "status" ].include?(ARGV.first)
  install_dependent_roles
end

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.hostname = "geowave-vagrant"
  config.vm.host_name = "geowave-vagrant"
 
  config.ssh.username = "vagrant"
  config.ssh.forward_agent = true

  # Port forwarding for Geoserver
  config.vm.network :forwarded_port, guest: 8080, host:8080

  # Setup a synced folder in the current directory
  config.vm.synced_folder "./geoserver", "/home/vagrant/geoserver", create: true

  # VirtualBox settings
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", 4096]
    vb.customize ["modifyvm", :id, "--cpus", 2]
    vb.customize ["modifyvm", :id, "--ioapic", "on"]
    vb.name = "geoserver-vagrant"
    vb.gui = true
  end

  # Ansible provisioning
  config.vm.provision :ansible do |ansible|
    ansible.playbook = "ansible/site.yml"
    ansible.groups = { "default" => ["default"] }
    ansible.extra_vars = { ansible_ssh_user: 'vagrant' }
  end
end

