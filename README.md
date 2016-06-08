# npm-wordpress

This plugin is used with vagrant

If you want to be able to push to github from the shared vagrant folders, you'll need to add ssh keys to your github account. https://help.github.com/articles/checking-for-existing-ssh-keys/

```
 # check to see if you have any existing keys
 ls -al ~/.ssh

 # if you don't, make some new ones. Make sure to add a passphrase because that's what github wants you to do
 ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

 # Add your keys to the ssh-agent
 eval "$(ssh-agent -s)"
$ ssh-add ~/.ssh/id_rsa

# Add your new public key to your github account
# Follow this link https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/

```

Something else you'll possibly need to do is make sure you can ssh from your virtualbox guest through the host. You may need to make an entry in your `~/.ssh/config` file that looks something like this

```
Host  *
      ForwardAgent  yes
```

This allows ssh traffic to be forwarded through the host machine.