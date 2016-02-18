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

        ####
        ## VirtualBox
        ####
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

        ####
        ## base server configuration
        ####

        # call base provisioner
        # config.vm.provision :shell, privileged: false, path: "#{scripts_url}/base"

        ####
        ## mysql
        ####

        # @param: database name
        args_mysql_db_name = "dev"

        # @param: database user to create
        args_mysql_db_user = "dev"

        # @param: database user's password
        args_mysql_db_password = "dev"

        # @param: allowed hostname for connection to new database
        args_mysql_db_host = "localhost"

        # call mysql provisioner
        #config.vm.provision :shell, privileged: false, path: "#{scripts_url}/mysql", args: [ args_mysql_db_name, args_mysql_db_user, args_mysql_db_password, args_mysql_db_host ]


        ####
        ## php
        ##
        ## - Specify any version of php >= 5.3. I recommend using 5.5 or 5.6
        ##   since they don't need phpbrew to install
        ## - If you are comfortable with phpbrew, you can also specify semantic
        ##   versions (e.g. 5.4.40)
        ####

        # @param: version of php to install
        args_php_version = "5.6"

        # @param: list of php packages to install, note: if using PhpBrew, make sure you use the available variants. E.g. "+default +fpm +gd". For more info, check the cookbook: https://github.com/phpbrew/phpbrew/wiki/Cookbook
        args_php_package_list = "php5-mcrypt php5-fpm"

        # @param: (optional) user to run php-fpm as, note: if left blank, user will be left as default
        args_php_user = "vagrant"

        # @param: (optional) group to run php-fpm as, note: if left blank, group will be left as default
        args_php_group = "vagrant"

        # call php provisioner
        #config.vm.provision :shell, privileged: false, path: "#{scripts_url}/php", args: [ args_php_version, args_php_package_list, args_php_user, args_php_group ]


        ####
        ## nginx
        ####

        # @param: path to the document root
        args_nginx_document_root = "/vagrant/public"

        # @param: hostname of the application
        args_nginx_hostname = "_"

        # @param: local ip address of the application
        args_nginx_ip_address = ""

        # @param: (optional) user to run nginx as, note: if left blank, user will be left as default
        args_nginx_user = "vagrant"

        # @param: (optional) group to run nginx as, note: if left blank, group will be left as default
        args_nginx_group = "vagrant"

        # call nginx provisioner
        #config.vm.provision :shell, privileged: false, path: "#{scripts_url}/nginx", args: [ args_nginx_document_root, args_nginx_hostname, args_nginx_ip_address, args_nginx_user, args_nginx_group ]


        ####
        ## ruby
        ## 
        ## 
        ##
        ####

        # @param: version of ruby to install
        args_ruby_version = "2.3"

        # @param: (optional) user to run ruby as, note: if left blank, user will be left as default
        args_ruby_user = ""

        # @param: (optional) group to run ruby as, note: if left blank, group will be left as default
        args_ruby_group = ""

        # call ruby provisioner
        # config.vm.provision :shell, privileged: false, path: "#{scripts_url}/ruby", args: [ args_ruby_version, args_ruby_user, args_ruby_group ]




        ####
        ## composer
        ####

        # @param: (optional) location to run `composer install`
        args_composer_install_dir = ""

        # call composer provisioner
        #config.vm.provision :shell, privileged: false, path: "#{scripts_url}/composer", args: [ args_composer_install_dir ]
end
