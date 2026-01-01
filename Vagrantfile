ENV.delete('SSH_AUTH_SOCK')

Vagrant.configure(2) do |config|

  config.vm.provider "virtualbox" do |v|
    v.name = "homeserver"
    v.memory = 8192
    v.cpus = 4
    v.linked_clone = true
    v.check_guest_additions = false
  end

  config.vm.define "homeserver" do |h|
    h.vm.box = "ubuntu/jammy64"

    h.vm.network :forwarded_port, guest: 80, host: 80
    h.vm.network :forwarded_port, guest: 443, host: 443

    # TODO: setup syned docker images folder
    # h.vm.synced_folder "src/", "/srv/website"

    # NOTE: Check if ansible recognizes name as label
    h.vm.disk :disk, size: "5GB", name: "ssd1"
    h.vm.disk :disk, size: "5GB", name: "ssd1"
    h.vm.disk :disk, size: "5GB", name: "ssd2"
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "run.yml"
  end

end
