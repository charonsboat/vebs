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
gh_branch = "script/rails" # if you want to ensure consistency, use a specific tag (e.g. v0.1.0)
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
    config.vm.network :forwarded_port, guest: 3000,  host: 3000
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
    ## - Uncomment the Necessary scripts
    ##
    ######

        ####
        ## base server configuration
        ####

        # call base provisioner
        config.vm.provision :shell, privileged: false, path: "#{scripts_url}/base"


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
        # config.vm.provision :shell, privileged: false, path: "#{scripts_url}/mysql", args: [ args_mysql_db_name, args_mysql_db_user, args_mysql_db_password, args_mysql_db_host ]


        ####
        ## postgresql
        ####

        # @param: version of postgresql to install. leave blank to use the latest version
        args_pg_version = ""

        # call postgresql provisioner
        # config.vm.provision :shell, privileged: false, path: "#{scripts_url}/rails", args: [ args_pg_version ]


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

        # @param: (optional) list of php packages to install, note: if using PhpBrew, make sure you use the available variants. E.g. "+default +fpm +gd". For more info, check the cookbook: https://github.com/phpbrew/phpbrew/wiki/Cookbook
        args_php_package_list = "php5-mcrypt php5-fpm php5-mysql"

        # @param: (optional) user to run php-fpm as, note: if left blank, user will be left as default
        args_php_user = "vagrant"

        # @param: (optional) group to run php-fpm as, note: if left blank, group will be left as default
        args_php_group = "vagrant"

        # @param: (optional) owner to run php-fpm as, note: if left blank, owner will be left as default
        args_php_owner = "vagrant"

        # call php provisioner
        # config.vm.provision :shell, privileged: false, path: "#{scripts_url}/php", args: [ args_php_version, args_php_package_list, args_php_user, args_php_group, args_php_owner ]


        ####
        ## composer
        ####

        # @param: (optional) location to run `composer install`
        args_composer_install_dir = ""

        # call composer provisioner
        # config.vm.provision :shell, privileged: false, path: "#{scripts_url}/composer", args: [ args_composer_install_dir ]


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
        # config.vm.provision :shell, privileged: false, path: "#{scripts_url}/nginx", args: [ args_nginx_document_root, args_nginx_hostname, args_nginx_ip_address, args_nginx_user, args_nginx_group ]


        ####
        ## node
        ####

        # @param: version of node to install (e.g. 4.2.1). defaults to 'node' for the latest stable version
        args_node_version = "node"

        # @param: global node packages to install
        args_node_packages = "npm pm2 gulp"

        # call node provisioner
        # config.vm.provision :shell, privileged: false, path: "#{scripts_url}/node", args: [ args_node_version, args_node_packages ]


        ####
        ## npm
        ####

        # @param: (optional) location to run `npm install`
        args_npm_install_dir = "/vagrant"

        # call npm provisioner
        # config.vm.provision :shell, privileged: false, path: "#{scripts_url}/npm", args: [ args_npm_install_dir ]


        ####
        ## ruby
        ##
        ## - installs only ruby. to install ruby on rails use the rails script
        ##   below.
        ## - installs using rbenv
        ####

        # @param: version of ruby to install. rbenv requires the exact version number, and a list of all support versions is available with the command "rbenv install -l"
        args_ruby_version = "2.3.0"

        # @param: list of ruby packages to install. see script for list of packages already specified for install.
        args_package_list = ""

        # call ruby provisioner
        # config.vm.provision :shell, privileged: false, path: "#{scripts_url}/ruby", args: [ args_ruby_version, args_package_list ]


        ####
        ## rails
        ##
        ## - built on ruby rbenv, use those commands to switch ruby versions
        ## - currently only installs latest ruby and latest rails.
        ## - newer rails is build on newer ruby versions:
        ##   rails 5   => ruby 2.2.2
        ##   rails 4   => ruby 1.9.3
        ##   rails 3.2 => ruby 1.8.7
        ####

        # @param: version of ruby to install (e.g. 2.3.0)
        args_ruby_version = "2.2.2"

        # @param: version of rails to install (e.g. 4.2.5)
        args_rails_version = "4.2.5"

        # @param: list of rails packages to install. see script for list of packages already specified for install.
        args_package_list = ""

        # call rails provisioner - ruby installation requires a reboot, so uncomment all three of these lines
        # config.vm.provision :shell, privileged: false, path: "#{scripts_url}/rails", args: [ args_ruby_version, args_rails_version, args_package_list ]
end
