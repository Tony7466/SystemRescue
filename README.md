# SystemRescue

## Project website
Homepage: https://www.system-rescue.org/

## Project sources
This git repository contains SystemRescue sources files. This is based on
https://gitlab.archlinux.org/archlinux/archiso/

## Building SystemRescue
SystemRescue can be built for x86_64 or i686 architectures. It must be built
on archlinux if you want to build a 64bit edition, or archlinux32 if you want
to create a 32bit edition. The following packages must be installed on the
build system: archiso, grub, mtools, edk2-shell, hugo. You need to use a modified
version of archiso for the build to work and for additional fixes and features
to be present. You can find the required archiso version and patches in the
"patches" folder in this git repository.

The package list contains packages which are not part of the official binary
package repositories. These packages need to be built from sources from the AUR
website. These sources are made of at least a PKGBUILD file and quite often
other related files, such as patches. These can be built using the makepkg
command which generates binary packages. These binary packages must be copied to
a custom package repository which can be hosted locally using httpd or nginx.
The repo-add command must be used to generate the repository package index.
The pacman.conf file must be updated with the address of this repository so
custom packages can be accessed.

The build process requires the systemrescue-website repository which is included
as git submodule. So when checking out this repository, make sure to check out
the submodule too. This can be done for example with
`git clone --recurse-submodules https://gitlab.com/systemrescue/systemrescue-sources.git`

The build process can be started by running the build.sh script. It will create
a large "work" sub-directory and the ISO file will be written in the "out"
sub-directory.

If you are not running archlinux, you can run the build process in docker.
You need to have a Linux system running with docker installed and configured.
You can use the scripts provided in the `docker` folder of this repository.
First you need to run the script which builds a new docker image, and then you
need to run the script which uses this docker image to builds the ISO image.

## Including your SystemRescueModules
If you want to include your own [SystemRescueModules][srm], place their srm files
in the [srm](./srm) directory of the repository before running the build script.

[srm]: https://www.system-rescue.org/Modules/
