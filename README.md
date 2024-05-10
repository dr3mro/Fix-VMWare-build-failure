# Fix-VMWare-build-failure
causes system isnatbility and freeze but build is successful
```
#!/bin/sh

# switch to the vmmware modules source dir
cd /usr/lib/vmware/modules/source/

# create backup of the modules
cp vmmon.tar vmmon.tar.bak

# extract the module with code issue 
tar -xvf vmmon.tar 

# fix the line that caused the build to fail
sed  -i "s/asm\/timex/uapi\/linux\/timex/" vmmon-only/common/vmx86.c 

# package the module again
tar -cvf vmmon.tar vmmon-only

# remove the working dir 
rm -rf vmmon-only

# try to rebuild the module 
vmware-modconfig --console --install-all
```
