<html><body><p>“embdemid GNU/Linux” is an embedded-linux project based on emdebian for mobile internet devices like Compal JAX 10,Aigo P8860,Aigo P8888."embdemid linux" can be installed on usb flash memories.It's an embedded distro which can perfectly work wired and wireless internet on Compal and Aigo MIDs.My tryings are still continue to run bluetooth function.If you have got a MID too, i strongly recommend you to try this distro.”embdemid linux” was configured for MID but with a couple of changes you can also work it on all x86 platforms.You can download ”embdemid linux” from “<a href="http://sourceforge.net/projects/embdemid/" target="_blank">http://sourceforge.net/projects/embdemid/</a>”
</p><h3>Installing Embdemid Linux on USB Flash Memory:</h3>
<strong>1-</strong>Firstly download the file named "embdemid-0.0.1.tar.bz2(56 MB)" from the internet address above.Then extract it;

$ <em>tar xjvf  embdemid-0.0.1.tar.bz2</em>

<strong>2-</strong>Prepare our USB Flash memory for downloading.(it should at least 180 MB space)

# <em>su</em>

#<em> fdisk -l</em>

# <em>umount /dev/sda1</em> (if usb flash disc mounted the system)

I'm using the “/dev/sda” device as a sample.It can be different in your system.

# <em>fdisk /dev/sda</em>

<em>&gt; d </em>(with this command erase the previous partitions.if there is more than one partition erase them all with ” d ”)


<em>&gt;p</em> (with this command, be sure that all partitions in flash disc are erased)


<em>&gt; n ,  p  ,  1 , enter , enter</em> (make these commands step by step.don't forget we are in fdisc programme!)

<em>&gt; p </em>(be sure that our partition is emerged)

<em>&gt;w</em>



<em>3-</em>If you applied the steps above, partition which is in your flash disc need to be ready and we can format this partition with ext2.

# <em>mkfs.ext2 /dev/sda1</em>

# <em>tune2fs -i 0 /dev/sda1</em>


<strong>4-</strong>Mount our USB Flash disc to the system.

# <em>mkdir /mnt/flash</em>

# <em>mount -t ext2 /dev/sda1 /mnt/flash</em>


<strong>5-</strong>Copy the downloaded “embdemid-0.0.1″ contents on flash disc.

# <em>cp -r /your-path/embdemid-0.0.1/* /mnt/flash</em>



<em>6-</em>Finally, we load a group on flash disc.

# <em>echo ‘(hd0) /dev/sda’ &gt; /mnt/flash/boot/grub/device.map</em>

# <em>grub-install –root-directory=/mnt/flash /dev/sda</em>

Note:There are two default users:
<strong>1-root
password:embedded
2-linux
password:123456</strong>

All steps are done, your system is ready, mount the flash disc to MID and test it.Have fun:)</body></html>