# -*- mode: ruby -*-
# vi: set ft=ruby :


####
## GitHub Configuration
######

gh_user   = "drmyersii"
gh_repo   = "vagrant-env-basher"
gh_branch = "master"
gh_url    = "https://raw.githubusercontent.com/#{gh_user}/#{gh_repo}/#{gh_branch}"

# path to scripts
scripts_url = "#{gh_url}/scripts"


####
## Vagrant Configuration
######

Vagrant.configure(2) do |config|

    # set the base box
    config.vm.box = "ubuntu/trusty64"

    # set up network configuration
    config.vm.network :forwarded_port, guest: 80,  host: 10080
    config.vm.network :forwarded_port, guest: 443, host: 10443

    ####
    ## Provisioning Configuration
    ##
    ## - Comment the Unnecessary scripts
    ## - Uncomment the Necessary scripts
    ######

    ## php
    ####
    args_php_version = "5.5.17"
    config.vm.provision :shell, path: "#{scripts_url}/php", args: [ args_php_version ]
end
