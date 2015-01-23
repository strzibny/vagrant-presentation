# Vagrant Presentation

This is the accompanying text to the Vagrant presentation available
in this repository with comprehensive and structured information
featured in the slides.

Note: This presentation and text talks primarily about using
Vagrant with libvirt provider (which is provided by vagrant-libvirt
plugin) on Fedora and derivates. A lot of the information is general
though.


## Creating a Vagrant box

### From Scratch

To create a desired image for your Vagrant box you need to ensure that
vagrant user with sudo right and without password protection exists.

Vagrant will use this vagrant user to access your virtual machine via
SSH which means that SSH has to present in the VM and properly set up.

To do so on CentOS 6 one has to install openssh-server package, start
and enable the service:

```shell
# yum install openssh-server
# service sshd start
# chkconfig sshd on
# netstat -tulpn | grep :22
```

For Fedora 21 server is this already done by default so this step can
be skipped.

To set up SSH access with insecure Vagrant public keys, run:

```shell
$ mkdir .ssh
$ curl -k https://raw.github.com/mitchellh/vagrant/master/keys/vagrant.pub
> .ssh/authorized_keys
$ chmod 0700 .ssh
$ chmod 0600 .ssh/authorized_keys
```

And ensure that vagrant user has no password:

You can do that on Fedora with visudo command:

<pre><code data-trim contenteditable>
# No password
%vagrant ALL=(ALL) NOPASSWD: ALL
...
# No requiretty, Fedora default
# Defaults    requiretty
...
# SSH agent forwarding
Defaults env_keep += "SSH_AUTH_SOCK"
</code></pre>


- how to use Vagrant as a developer
- how to create a custom box from scratch
- how to create a box easily
- where to find boxes
- Vagrant packaging efforts for Fedora
- demo
