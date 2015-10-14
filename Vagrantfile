# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure(2) do |config|

    ####
    ## Vagrant Configuration
    ######

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
end
