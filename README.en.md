# Fedora-RISCV-Builder

## Getting Started

### Supported SBCs

* [LicheePi-4A (8+8 Developer Edition)](./doc/install-guild-licheepi4a.md)

### Build Manually

```
git clone https://github.com/chainsx/fedora-riscv-builder.git && cd fedora-riscv-builder
bash build.sh
```

### Download Pre-built Systems

[Release](https://github.com/chainsx/fedora-riscv-builder/releases)

* Username: `root`
* Password: `fedora`

----

### Instructions

The project requires a file named `fedora-38-core-rootfs.tar.gz` to be built using a Fedora 38 host with the RISC-V architecture. The build process is as follows. If you do not wish to build it yourself, you can use the pre-built file provided by the project.

```
sudo su && cd ~
WORKDIR=$(pwd)

cd $WORKDIR
mkdir rootfs
mkdir -p rootfs/var/lib/rpm
rpm --root  $WORKDIR/rootfs/ --initdb

rpm -ivh --nodeps --root $WORKDIR/rootfs/ http://fedora.riscv.rocks/repos-dist/f38/latest/riscv64/Packages/f/fedora-release-38-34.noarch.rpm

mkdir -p $WORKDIR/rootfs/etc/yum.repos.d
cp /etc/yum.repos.d/*repo $WORKDIR/rootfs/etc/yum.repos.d
dnf --installroot=$WORKDIR/rootfs/ install dnf --nogpgcheck -y

cd $WORKDIR/rootfs
tar -zcvf fedora-38-core-rootfs.tar.gz .
```

This way, you will obtain the `fedora-38-core-rootfs.tar.gz` file required for the project script in the `/root` directory.
