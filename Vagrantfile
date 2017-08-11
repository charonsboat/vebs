# -*- mode: ruby -*-
# vi: set ft=ruby :


####
##
## GitHub Configuration
##
######

# if you want to maintain your own version of this project, feel free to
# fork it and change the following to reflect your own copy
gh_user   = "drm2"
gh_repo   = "vebs"
gh_branch = "v0.12.0" # the latest tag is specified to ensure consistency (you may also use "master", but future changes may cause errors in your environment)
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

max_memory = 1536

Vagrant.configure(2) do |config|

    config.vm.define "vebs" do |vebs|

        # set the base box
        vebs.vm.box = "ubuntu/trusty64"

        # set up network configuration
        vebs.vm.network :forwarded_port, guest: 80,  host: 10080
        vebs.vm.network :forwarded_port, guest: 443, host: 10443


        ####
        ## VirtualBox
        ####

        vebs.vm.provider "virtualbox" do |provider, override|
            provider.memory = max_memory
            provider.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/vagrant", "1"]
        end

        ####
        ## Digital Ocean
        ####

        vebs.vm.provider "digital_ocean" do |provider, override|
            # optionally use rsync to mount shared folder
            # override.vm.synced_folder ".", "/vagrant", type: "rsync", rsync__exclude: [ ".vagrant", ".git" ]

            # you probably don't need to change these
            override.vm.box = "digital_ocean"
            override.vm.box_url = "https://github.com/devopsgroup-io/vagrant-digitalocean/raw/master/box/digital_ocean.box"

            # configure the DO droplet here
            override.ssh.private_key_path = ENV["DIGITAL_OCEAN_PRIVATE_SSH_KEY"] || "~/.ssh/id_rsa"
            provider.token = ENV["DIGITAL_OCEAN_ACCESS_TOKEN"] || "use ENV or set access token here"
            provider.image = "ubuntu-14-04-x64"
            provider.region = "nyc3"
            provider.size = "512mb"

            # optional droplet configuration
            # override.ssh.username = "set ssh user here"
            # provider.ssh_key_name = "Vagrant"
            # provider.setup = true
            # provider.ipv6 = true
            # provider.private_networking = false
            # provider.backups_enabled = false
        end


        ####
        ## base server configuration
        ####

        # @param: (optional) list of system packages to install separated by spaces. E.g. "git curl screen"
        args_base_packages = "git zip unzip"

        # @param: (optional) locale to set for LC_ALL global
        args_base_locale = "en_US.UTF-8"

        # call base provisioner
        config.vm.provision :shell, privileged: false, path: "#{scripts_url}/base", args: [ args_base_packages, args_base_locale ]

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

        # @param: database name
        args_postgresql_db_name = "dev"

        # @param: database user to create
        args_postgresql_db_user = "dev"

        # @param: database user's password
        args_postgresql_db_password = "dev"

        # @param: allowed hostname for connection to new database
        args_postgresql_db_host = "localhost"

        # call postgresql provisioner
        # config.vm.provision :shell, privileged: false, path: "#{scripts_url}/postgresql", args: [ args_postgresql_db_name, args_postgresql_db_user, args_postgresql_db_password, args_postgresql_db_host ]

        ####
        ## php
        ####

        # @param: version of php to install (must be 5.5, 5.6, or 7.0)
        args_php_version = "5.6"

        # @param: (optional) list of php extensions to install, note: due to the new PPA, you will need to specify the version of php in the extension names as well
        args_php_extensions = "php5.6-cli php5.6-mcrypt php5.6-fpm php5.6-mysql php5.6-mbstring php5.6-xml php5.6-zip"

        # @param: (optional) user to run php-fpm as, note: if left blank, user will be left as default
        args_php_user = "vagrant"

        # @param: (optional) group to run php-fpm as, note: if left blank, group will be left as default
        args_php_group = "vagrant"

        # @param: (optional) owner to run php-fpm as, note: if left blank, owner will be left as default
        args_php_owner = "vagrant"

        # call php provisioner
        # config.vm.provision :shell, privileged: false, path: "#{scripts_url}/php", args: [ args_php_version, args_php_extensions, args_php_user, args_php_group, args_php_owner ]

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
        ####

        # @param: version of ruby to install (e.g. 2.3.0). defaults to 'ruby' for the latest stable version
        args_ruby_version = "ruby"

        # @param: (optional) list of ruby packages to install. the '--no-rdoc' and '--no-ri' flags disable documentation generation to help speed up the install process for gems.
        args_ruby_package_list = "--no-rdoc --no-ri bundler rails"

        # call ruby provisioner
        # config.vm.provision :shell, privileged: false, path: "#{scripts_url}/ruby", args: [ args_ruby_version, args_ruby_package_list ]

        ####
        ## go
        ####

        # @param: version of go to install (e.g. 1.6).
        args_go_version = "1.6"

        # @param: (optional) path to set for $GOPATH
        args_go_gopath = "/home/vagrant/go"

        # call go provisioner
        # config.vm.provision :shell, privileged: false, path: "#{scripts_url}/go", args: [ args_go_version, args_go_gopath ]

        ####
        ## rust
        ####

        # @param: version of rust to install (e.g. 1.11.0).
        args_rust_version = "1.11.0"

        # call rust provisioner
        # config.vm.provision :shell, privileged: false, path: "#{scripts_url}/rust", args: [ args_rust_version ]
    end
end
