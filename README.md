# testGREP

VM to test [GREP](https://github.com/matthieurenard/GREP).
This VM is set up using [Vagrant](https://vagrantup.com).
To use it, you first need to install the following tools:
* Vagrant
* VirtualBox
* VirtualBox extension pack

## Installing Vagrant

To install Vagrant, use a package manager (this is not recommended since 
packages are often out of date), or go to [Vagrant download 
page](https://vagrantup.com/downloads.html) and choose the download 
corresponding to your configuration (For Ubuntu users, the Debian package should 
work).

## Installing VirtualBox and Extension Pack

VirtualBox can also be installed from repositories on certain distributions, or 
from [VirtualBox download page](https://www.virtualbox.org/wiki/Downloads).
The Extension Pack can also be found on this page.
To install the Extension Pack, first install VirtualBox and then open the 
Extenstion Pack with VirtualBox.

## Running the Virtual Machine

Once Vagrant, VirtualBox, and the Extension Pack are installed, open a 
shell, go to some directory that will contain this git repository, and issue:
```
git clone https://github.com/matthieurenard/testGREP.git
```
then cd into the testGREP repository:
```
cd testGREP
```
Verify that the Vagrantfile is in the current working directory with `ls`.
If you do not want to use *git*, you can simply download the Vagrantfile 
directly at the url 
https://raw.githubusercontent.com/matthieurenard/testGREP/master/Vagrantfile.
For example, using wget:
```
wget https://raw.githubusercontent.com/matthieurenard/testGREP/master/Vagrantfile
```
You can also download a zipped version of the repository from github.
The only important thing is that you have the Vagrantfile in the current working 
directory of your shell.
Then, run:
```
$ vagrant up
```

This should download the Virtual Machine and launch it.
Once the VM has started (there is no graphical interface, the command line 
should just return a new prompt), issue

```
$ vagrant ssh
```

to log into the Virtual Machine.

To test GREP, go to the GREP/tests/offline directory:

```
$ cd ~/GREP/tests/offline
```

The executable *game_enf_offline* is GREP running in offline mode.
Some properties are already given in the directory (files with extension .tmtn).
To test GREP on property *propThesis.tmtn* for instance, with input (1, w)(2, 
a)(3, on)(4, w)(5, off), issue:

```
$ echo "(1, w)(2, a)(3, on)(4, w)(5, off)" | ./game_enf_offline -a propThesis.tmtn
```

To also draw the game graph and the zone graph, one can use:

```
$ echo "(1, w)(2, a)(3, on)(4, w)(5, off)" | ./game_enf_offline -a propThesis.tmtn -d gamegraph.pdf -z zonegraph.pdf
```

Since there is no graphical interface in the VM, to see the produced files, we 
need to retrieve them on the host.
To do this, simply copy or move the files to the directory /vagrant, which is 
synced with the directory of the host containing the Vagrantfile:

```
$ cp gamegraph.pdf zonegraph.pdf /vagrant
```

The files should appear on the host next to the Vagrantfile.
Use your favourite PDF viewer to visualise them.

You can leave the virtual machine just like any SSH connection, by simply 
issuing:
```
exit
```


