Multipass is the recommended method to create Ubuntu VMs on Ubuntu. It’s designed for developers who want a fresh Ubuntu environment with a single command and works on Linux, Windows and macOS.

## Find available images
```
$ multipass find
```

## Launch a fresh instance of the current Ubuntu LTS
```
$ multipass launch --name ubuntu-lts
```

## Check out the running instances
```
$ multipass list
```
## Learn more about the VM instance you just launched
```
$ multipass info ubuntu-lts
```
## Connect to a running instance
```
$ multipass shell ubuntu-lts
```
## Run commands inside an instance from outside
```
$ multipass exec ubuntu-lts -- lsb_release -a
```
## Stop an instance to save resources
```
$ multipass stop ubuntu-lts
```
## Delete the instance
```
$ multipass delete ubuntu-lts
```
It will now show up as deleted:

Name                    State             IPv4             Release
snapcraft-asciinema     STOPPED           --               Ubuntu Snapcraft builder for Core 18
ubuntu-lts              DELETED           --               Not Available

## And when you want to completely get rid of it:
```
$ multipass purge
```
Integrate into the rest of your virtualization

You might have other virtualization already based on libvirt either through using the similar older uvtool already or through the common virt-manager.

You might for example want those guests to be on the same bridge to communicate to each other or you need access to the graphical output for some reason.

## Fortunately it is possible to integrate this by using the libvirt backend of multipass
```
$ sudo multipass set local.driver=libvirt
```
## After that when you start a guest you can also access it via tools like virt-manager or virsh
```
$ multipass launch ubuntu-lts
```
## Launched: ubuntu-lts
```
$ virsh list
```
 Id    Name                           State
----------------------------------------------------
 15    ubuntu-lts                     running

## Get help
```
multipass help
```
multipass help <command>
