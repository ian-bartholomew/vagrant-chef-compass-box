# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant::Config.run do |config|
  config.vm.box = "CentOS_64"
  config.vm.box_url = "http://puppet-vagrant-boxes.puppetlabs.com/centos-64-x64-vbox4210.box"

  # config.vm.box       = 'precise32'
  # config.vm.box_url   = 'http://files.vagrantup.com/precise32.box'
  config.vm.host_name = 'chef-ruby-box'

  # config.vm.network :hostonly, "192.168.30.00"
  config.vm.share_folder("vagrant-root", "/vagrant", ".", "nfs" => true)

  config.vm.forward_port 80, 8080

  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = ["chef/cookbooks", "chef/site-cookbooks"]
    chef.roles_path     = [[:host, "chef/roles"]]
    chef.data_bags_path = [[:host, "chef/data_bags"]]

    chef.add_role "ruby-development"
    chef.json = {
        "rbenv" => {
          "global"  => "2.0.0-p0",
          "rubies" => [ "2.0.0-p0" ],
          "gems" => {
            "2.0.0-p0" => [
              { 'name' => 'bundler' },
              { 'name' => 'compass' },
            ]
          }
        },
        "apache" => {
          "default_site_enabled" => true,
          # change project-files to the root of your checked out project
          "docroot_dir" => "/vagrant/project-files"
        }
      }

  end
end
