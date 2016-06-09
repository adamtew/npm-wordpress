This project uses vagrant for the wordpress environment.

To setup vagrant for editing the project perform the following.

```bash
# Make sure you have virtualbox and vagrant installed
# get the .zip file from http://vccw.cc/
# unzip the .zip file, rename the folder to perfumania, and move it where you want the repo to reside
unzip ~/Downloads/vccw-2.21.0.zip -d ~/{dev}/pxp200/perfumani

# create a new site.yml file
cd ~/{dev-environment}/pxp200/perfumania
cp provision/default.yml  site.yml

# Open site.yml and change the hostname and ip address
# It's important to change these if the defaults will conflict 
# hostname: perfumania.dev
# ip: 192.168.33.11
# reset_db_on_provision: false

# setup the vagrant box
vagrant up

```

The next thing you'll want to do is get the repo setup for editing inside the shared folders. If you want to be able to push to github from the shared vagrant folders, you'll need to add ssh keys to your github account. https://help.github.com/articles/checking-for-existing-ssh-keys/

```bash
# log into the guest machine
vagrant ssh

# check to see if you have any existing keys
 ls -al ~/.ssh

# if you don't, make some new ones. Make sure to add a passphrase because that's what github wants you to do
 ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

# Add your keys to the ssh-agent
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa

# Add your new public key to your github account
# Follow this link https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/

# test your connection
ssh -T git@github.com

# success means you passed

```

Something else you'll possibly need to do is make sure you can ssh from your virtualbox guest through the host. You may need to make an entry in your `~/.ssh/config` file that looks something like this

```bash
Host  *
      ForwardAgent  yes
```

This allows ssh traffic to be forwarded through the host machine.