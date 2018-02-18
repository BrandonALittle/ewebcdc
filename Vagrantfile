# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'fileutils'
require 'open-uri'
require 'tempfile'
require 'yaml'

Vagrant.require_version ">= 1.6.0"

Vagrant.configure(2) do |config|

  # always use Vagrant's insecure key
  config.ssh.insert_key = false

  config.vm.box="bento/ubuntu-16.04"

  # plugin conflict
  if Vagrant.has_plugin?("vagrant-vbguest") then
    config.vbguest.auto_update = false
  end

  # Base box
  config.vm.define :project do |project_config|
    project_config.vm.synced_folder ".", "/opt/project"
    project_config.vm.network :forwarded_port, host: 80, guest: 4000

    project_config.vm.provision :shell, :inline => "apt-get update && apt-get -y install ruby ruby-dev g++ libffi-dev", :privileged => true
    project_config.vm.provision :shell, :inline => "gem install jekyll bundle", :privileged => true
  end

end
