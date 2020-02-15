<html><body><img class="alignright" title="OpenSolaris" src="http://4.bp.blogspot.com/_b7TOyTq06Us/SvxiLBRV6eI/AAAAAAAAAZ4/epfS5wbNuFc/s200/opensolaris.jpg" alt="" width="200" height="200">OpenSolaris ile bugünlerde haşır neşir oluyorum ve bazı noktaları buraya not düşüyorum.OpenSolaris ile ext2 ve ext3 disk bölümlerini bağlamak için gereken adımlar:

1. <a title="FSWpart" href="http://www.belenix.org/binfiles/FSWpart.tar.gz">FSWpart</a>

<a title="FSWmisc" href="http://www.belenix.org/binfiles/FSWfsmisc.tar.gz">FSWfsmisc </a>

Yukardaki iki paketi indirin.

2. " tar xvf  <span style="font-family: courier new,courier,monospace;">FSWpart.tar.gz " ve " tar xvf </span><span style="font-family: courier new,courier,monospace;">FSWfsmisc.tar.gz" komutları ile paketleri açın.</span>

<span style="font-family: courier new,courier,monospace;">3.root olun ve " pkgadd -d </span><span style="font-family: courier new,courier,monospace;">. FSWpart " ve " pkgadd -d . FSWfsmisc " komutları ile paketleri sisteme kurun.</span>

<span style="font-family: courier new,courier,monospace;">4." prtpart " komutu ile bağlı olun diskleri görüntüleyin.</span>

<span style="font-family: courier new,courier,monospace;">Örnek olarak:</span>

/dev/rdsk/c7d0p0
/dev/rdsk/c7d1p0

Yukardaki gibi sisteme bağlı diskler listelenecektir.

5.  " prtpart /dev/rdsk/c7d0p0 -ldevs " komutu ile diskin dosya sistemini öğrenelim.

Örnek:

Fdisk information for device /dev/rdsk/c7d0p0

** NOTE **
/dev/dsk/c7d0p0      - Physical device referring to entire physical disk
/dev/dsk/c7d0p1 - p4 - Physical devices referring to the 4 primary partitions
/dev/dsk/c7d0p5 ...  - Virtual devices referring to logical partitions

Virtual device names can be used to access EXT2 and NTFS on logical partitions

/dev/dsk/c7d0p1    Linux native

Yukarda gördüğünüz gibi " /dev/dsk/c7d0p1" diski bir linux dosya sistemi.Şimdi bu linux bölümünü  sistemimize bağlıyalım.

6. İlk önce bir bağlama noktası oluşturalım.

# mkdir /mnt/ext

ve şimdi diski bağlayalım.

# mount -F ext2fs /dev/dsk/c7d0p2 /mnt/ext

Kolay gelsin :)

<span style="font-family: courier new,courier,monospace;">
</span></body></html>