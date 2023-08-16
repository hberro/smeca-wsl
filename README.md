# smeca-wsl
Salome Meca additions after converting the official SIF images to WSL

This repository contains the Salome Meca additions to the official SIF image
of this software which allow to leverage its use in a WSL environment.

The additions include :

System scope
-------------

- Set environment for root and user in `/etc/profile`
- WSL configuration file in `/etc/wsl.conf`
- FSTAB defintion for the `/tmp` direction : tmpfs of 2GB (in `/etc/fstab`)
- Shortcut scripts to launching different salome_meca tools (in `/usr/local/smeca`)
- Deactivated services such as gdb session which can cause cpu/disk overkill
- Script for automatic useradd call (`smeca-user`, pwd: `code_aster`), set up as a 
  `systemd` service (in `/usr/sbin/create_default_user` & `create-default-user.service`)

User scope (smeca-user:smeca)
-----------------------------

- Home directory automatically set to `/mnt/c/smeca/data` at user creation with a
  symbolic link at /home/smeca-user (i.e. `C:\smeca\data`)
- `/etc/skel` customizations for the default user (and new users)
	1. .bashrc customized with a welcome and decoration headers
	2. containers folder in the home directory (use requires singularity install)


Singularity
-----------

These additions **do not** include the installation of singularity-ce which 
needs to be undertaken manually if the `cont_*` scripts are needed.


Possible (easy) customizations
-------------------------------

- Default username and home directory can be changed in :
	1. `/usr/sbin/`
	2. `/usr/local/smeca/welcome`

/etc/wsl.conf must be modified to set the new username as default.

- The size of the tmpfs (`/tmp`) can be changed easily by modifying `/etc/fstab`

For example, the following sets the /tmp folder size to 4GB...

```
tmpfs   /tmp    tmpfs   defaults,size=4G   0 0
```