# Vagrantfile с docker-провайдером (VirtualBox не работает на Apple Silicon).
Vagrant.configure("2") do |config|
  config.vm.provider "docker" do |d|
    d.image           = "ubuntu:22.04"
    d.name            = "lab10-dev"
    d.cmd             = ["tail", "-f", "/dev/null"]
    d.remains_running = true
    d.has_ssh         = false
  end

  config.vm.synced_folder "shared", "/vagrant", disabled: true
end
