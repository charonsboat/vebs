# vagrant-env-basher

Reusable Bash provisioning scripts for Vagrant (or other) environments.


## usage

To get started, all you need to do is pull down a copy of this project's Vagrantfile:

```bash
# wget
wget https://bitly.com/drmyersii-vagrantfile -O Vagrantfile
```

Now, you can uncomment the packages you need and launch Vagrant:

```bash
# launch vagrant
vagrant up
```

That's it! Enjoy!


## development

To develop/test scripts locally, you simply need to fork the repo and change the last command when launching Vagrant:

```bash
# launch vagrant in DEV mode
export ENV=DEV && vagrant up
```


Project inspired by Vaprobash
