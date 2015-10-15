# -*- mode: ruby -*-
# vi: set ft=ruby :


####
##
## GitHub Configuration
##
######

# if you want to maintain your own version of this project, feel free to
# fork it and change the following to reflect your own copy
gh_user   = "drmyersii"
gh_repo   = "vagrant-env-basher"
gh_branch = "master" # if you want to ensure consistency, use a specific tag (e.g. v0.1.0)
gh_url    = "https://raw.githubusercontent.com/#{gh_user}/#{gh_repo}/#{gh_branch}"

# path to provisioning scripts
scripts_url = "#{gh_url}/scripts"

# if environment is set to development, use local scripts instead
if ENV["ENV"] == "DEV"
    scripts_url = "./scripts"
end


####
##
## Vagrant Configuration
##
######

max_memory = 1024

Vagrant.configure(2) do |config|

    # set the base box
    config.vm.box = "ubuntu/trusty64"

    # set up network configuration
    config.vm.network :forwarded_port, guest: 80,  host: 10080
    config.vm.network :forwarded_port, guest: 443, host: 10443

    ####
    ##
    ## Provider Configuration
    ##
    ######

    #### VirtualBox

    config.vm.provider "virtualbox" do |v, override|
        v.memory = max_memory
        v.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/vagrant", "1"]
    end

    ####
    ##
    ## Provisioning Configuration
    ##
    ## - Comment the Unnecessary scripts
    ## - Uncomment the Necessary scripts
    ##
    ######

    #### base server configuration

    config.vm.provision :shell, privileged: false, path: "#{scripts_url}/base"


    ####
    ## php
    ##
    ## - Specify any version of php >= 5.3. I recommend using 5.5 or 5.6
    ##   since they don't need phpbrew to install
    ## - If you are comfortable with phpbrew, you can also specify semantic
    ##   versions (e.g. 5.4.40)
    ####
    args_php_version = "5.6"
    config.vm.provision :shell, privileged: false, path: "#{scripts_url}/php", args: [ args_php_version ]
end
