# Makeiso Animalism

This is a tool for making CentOS-7.4.1708 ISO of yourself.

This only works for CentOS-7.4.1708.

## Requirement

- An avaliable Linux platform. CentOS 7 is prefered, but Ubuntu is also OK
- A CentOS-7-x86_64-Everything-1708.iso image
- genisoimage (A RPM package is included in Everything 1708 iso image)
- createrepo (A RPM package is included in Everything 1708 iso image)
- rsync 3.1.1+ (not included in Everything 1708 iso image. A RPM package is included in this repository)

## Usage

Basic order:

1. Modify the GLOBAL VARIABLE if needed.
2. Copy addtional files you want to install after the system installation to `PAYLOAD_PATH`, and write a install.sh as the installation script.
3. Run makeiso.sh to generate iso file.

### GLOBAL VARIABLE

```
# INPUT
CENTOS7_EVERYTHING_ISO="/tmp/mountpoint/samba/share/CentOS-7-x86_64-Everything-1708.iso"
PAYLOAD_PATH="/root/payload_test/"
CONFIGDIR='boot.template/develop/'

# OUTPUT
OUTPUTFILEDIR="./"
VERSION="v1.0.0"
VOLUMENAME='PAYLOAD-'`date +'%Y%m%d%H%M'`-$VERSION
TIMEZONE='UTC'

# AUTO VARIABLE
VOLUMENAME_SHORT=`expr substr ${VOLUMENAME} 1 16`
FINALNAME=${VOLUMENAME}.iso
```

- **CENTOS7_EVERYTHING_ISO** MUST be a accessiable CentOS-7-x86_64-Everything-1708.iso files.
- **PAYLOAD_PATH** is addtional files you want to install after the system installation. After the system installation and auto reboot, `bash install.sh` will be execute automatically once.
- **VOLUMENAME_SHORT** is for Volume ID and it only support as long as 16 chars.

### Usage

```
Usage: ./makeiso.sh -d [DEST_DIR=./] -v [RELEASE_VERSION=v1.0.0] -s [PAYLOAD_PATH=/root/payload_test/] -7 [CENTOS7_EVERYTHING_ISO=/root/iso/CentOS-7-x86_64-Everything-1708.iso] -z [TIMEZONE=UTC]
```

And you will get a ISO file. The default username/password is root/root.

Notice that I enabled all the network interface DHCP in kickstart-post-script, so your network configuration in the Install Guide won't work.

* * *


## Build your own ISO

Anything doesn't relate to the CentOS-7-x86_64-Everything ISO is supposed to be put in PAYLOAD and be installed by install.sh

For something relates to the ISO, you can install a new CentOS7 by yourself, and run generatefilelist.sh to generate new rpm filelist, and upgrade kickstart.cfg and comps.xml by yourself. (Or just edit it in the Payload install.sh. It's fine)

This project is just for helping developers who don't familiar how to buid a CentOS ISO. You should write Kickstart-file (payload-develop.cfg) for your own project purpose.

## Other things

### Idea about naming this 'make linux iso project' Animalism

In day 1945.08.17, a novella was published. The name is *Animal Farm: A Fairy Story* . That's it.

### Idea about naming the directory Payload

See it in my another reposity ["Idea about naming the directory Payload"](https://github.com/catscarlet/makeiso-kuroko#user-content-idea-about-naming-the-directory-payload)

## References

- [GRUB 2 Custom Splash Screen on RHEL 7 UEFI and Legacy ISO Image](http://www.tuxfixer.com/set-grub2-custom-splash-screen-on-rhel-7-centos-7-uefi-and-legacy-bios-iso-image/)
- [Grub2/Displays](https://help.ubuntu.com/community/Grub2/Displays#Troubleshooting_Splash_Images)

## Contribution

Any contributions are welcome. Pull request to branch **dev** please.

## License

Makeiso-Animalism is licensed under MIT License.

The default splash image is from [""](https://commons.wikimedia.org/wiki/File:Flag_of_the_Animal_Farm.jpg#/media/File:Animalism_flag.svg) and it's licensed under a
["Creative Commons Attribution-Share Alike 3.0 Unported"](https://creativecommons.org/licenses/by-sa/3.0/deed.en)
