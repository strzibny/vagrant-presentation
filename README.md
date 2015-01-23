# Vagrant Presentation

This is the accompanying text to the Vagrant presentation available
in this repository with comprehensive and structured information
featured on the slides.

*Note: This presentation and text talks primarily about using
Vagrant with libvirt provider provided by vagrant-libvirt
plugin on Fedora and derivates. A lot of the information is general
though.*


## Creating a Vagrant box

### From Scratch

To create a desired image for your Vagrant box you need to ensure that
**vagrant** user with sudo rights and without password protection exists.

Vagrant will use this *vagrant* user to access your virtual machine via
SSH which means that SSH has to be present in the virtual machine and
properly set up.

To do so on CentOS 6, one has to install openssh-server package, start
and enable the service first:

```shell
# yum install openssh-server
# service sshd start
# chkconfig sshd on
# netstat -tulpn | grep :22
```

For Fedora 21 Server is this already done *by default* so this step can
be skipped.

Vagrant uses SSH keys to access the virtual machine so the public
keys needs to be present on the VM for *vagrant* user.

You can set them easily with the following commands for *vagrant* user:

```shell
$ mkdir .ssh
$ curl -k https://raw.github.com/mitchellh/vagrant/master/keys/vagrant.pub
> .ssh/authorized_keys
$ chmod 0700 .ssh
$ chmod 0600 .ssh/authorized_keys
```

Since Vagrant would do system provisioning and administration,
it needs to have sudo access on the machine. Using `visudo` command on Fedora
you can edit *sudoers* file and ensure that vagrant won't need a password
and have sudo rights with `%vagrant ALL=(ALL) NOPASSWD: ALL`.

When editing the *sudoers* file make sure that `requiretty` option is
not present (or it is commented out). That is the default on Fedora.
If you would require a real TTY then Vagrant commands sent to the VM
would fail.

Last option to set up when in *sudoers* file is to allow SSH agent
forwarding. You can set that up if you want to use the SSH key from
our local machine inside the Vagrant box.

```
# No password
%vagrant ALL=(ALL) NOPASSWD: ALL
...
# No requiretty, Fedora default
# Defaults    requiretty
...
# SSH agent forwarding
Defaults env_keep += "SSH_AUTH_SOCK"
```

A good practice is also setting up **root** user with password "vagrant",
although it is not necessary for Vagrant to work.


- how to use Vagrant as a developer
- how to create a custom box from scratch
- how to create a box easily
- where to find boxes
- Vagrant packaging efforts for Fedora
- demo
