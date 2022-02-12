DO_BOX_URL = "https://github.com/devopsgroup-io/vagrant-digitalocean/raw/master/box/digital_ocean.box"
PRIVATE_KEY_PATH = " " #your private key
TOKEN = " " #DO token


Vagrant.configure("2") do |config|
  config.vm.define "droplet1" do |droplet|
    droplet.vm.provider :digital_ocean do |provider, override|
      override.ssh.private_key_path = PRIVATE_KEY_PATH
      override.vm.box = 'digital_ocean'
      override.vm.box_url = DO_BOX_URL
      override.nfs.functional = false
      override.vm.allowed_synced_folder_types = :rsync
      provider.token = TOKEN
      provider.image = 'ubuntu-18-04-x64'
      provider.region = 'nyc1'
      provider.customize = ["modifyvm", :id, "--size", 25 * 1024]
      provider.memory = 1024
      provider.cpus = 2
    end
  config.vm.provision "ansible" do |ansible|
    ansible.verbose = "v"
    ansible.playbook = "playbook.yml"
    ansible.inventory_path = "inventory"
    ansible.limit = "localhost"
    end
  config.vm.provision "ansible" do |ansible|
    ansible.verbose = "v"
    ansible.playbook = "mount.yml"
    end
  end
end
