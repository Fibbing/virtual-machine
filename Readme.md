# Fibbing Virtual Machine

This is the virtual image definition to get a Fibbing controller installation.

Building it requires [Vagrant](vagrantup.com)

Using it requires [VirtualBox](virtualbox.org), although the Vagrantfile can be modified
to target other provider (see Vagrant Documentation).

# Building and starting the VM

```bash
DEST=fibbing-vm
git clone -o ${DEST} https://github.com/Fibbing/virtual-machine.git
cd ${DEST}
vagrant up
```

This will build a Debian virtual machine and add it to the list
of installed machines in VirtualBox.

# Accessing the VM

    1. Using ssh:
    ```
    vagrant ssh
    ```
    2. Using the VirtualBox frontend, login as user `vagrant` with password `vagrant`

# Misc. Info

When running the fibbingnode controller (e.g. sudo python -m fibbignode), be careful
with what physical interface you specify to be captured by the controller.
Capturing eht0 (to directly connect to a physical router for example) will
break your ssh session (if any) and prevent the root network namespace (= where you
land when accessing the VM) from accessing the outside networks.
