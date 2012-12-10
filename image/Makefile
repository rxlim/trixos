SIZE = 30M
IMAGEFILE = disk.img

all: image

$(IMAGEFILE):
	rm -f $@
	touch $@
	truncate -s $(SIZE) $@

image: $(IMAGEFILE)
	losetup /dev/loop0 $<
	losetup -a
	- echo -e "o\nn\np\n1\n2048\n+10M\na\n1\nw" | fdisk /dev/loop0
	- echo -e "n\np\n2\n22528\n61439\nw" | fdisk /dev/loop0
	losetup -o 1048576 --sizelimit 10485760 /dev/loop1 $<
	losetup -o 11534336 --sizelimit 19922944 /dev/loop2 $<
	mkfs.ext2 /dev/loop1
	mkfs.ext2 /dev/loop2
	rm -rf root
	mkdir root
	mount /dev/loop2 root
	mkdir root/boot
	umount root
	rm -rf root
	losetup -d /dev/loop{0,1,2}

.PHONY: $(IMAGEFILE)
