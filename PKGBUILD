# Maintainer: Stephano Cetola <stephanoc@gmail.com>

pkgname=linux-mnt-pocket
pkgver=6.17.11
pkgrel=2
_kernver="${pkgver}-mnt-pocket"
pkgdesc="Linux kernel for MNT Pocket Reform (arm64)"
arch=('aarch64')
url="https://github.com/cetola/mnt-build"
license=('GPL2')
depends=('dracut' 'kmod')
provides=('linux' 'linux-aarch64')
conflicts=('linux')
backup=('etc/modprobe.d/reform-qcacld2.conf')
source=(
  "kernel-${pkgver}-${pkgrel}-mnt.tar.gz::https://github.com/cetola/mnt-build/releases/download/${pkgver}-${pkgrel}-mnt-pocket/kernel-${pkgver}-${pkgrel}-mnt.tar.gz"
  "extlinux.conf.example"
  "mnt-pocket-initramfs.hook"
  "mnt-pocket-backup.hook"
  "mnt-pocket-backup.sh"
)
sha256sums=(
  '8703be8996bf7b2ee02e6632bce85d83f1842fa8060af5c60e02caadf0c6153c'
  '38fced8cce1d1c175c7a81b522af2ecdaee94735aa48aa4e9a29b75d2d75bd49'
  'c88373dffc2867c4f66d38e2958ac4ad97beab19225f1a3bd3bc1b98232bb8c7'
  'ca6b8f54f8a4933635b4e64328a17c172504729a075c38268cbdc8e861f1944b'
  'f073ad1a241603fb0ed53ca46e5bcf3da064ec53de9d854a41359ec9d76d858d'
)

options=(!strip !docs !emptydirs)

package() {
  cd "$srcdir"

  install -dm755 "$pkgdir/usr/lib/modules/${_kernver}"
  cp -r lib/modules/${_kernver}/* "$pkgdir/usr/lib/modules/${_kernver}/"

  install -Dm644 reform2_lpc.ko "$pkgdir/usr/lib/modules/${_kernver}/extra/reform2_lpc.ko"
  install -Dm644 wlan.ko        "$pkgdir/usr/lib/modules/${_kernver}/extra/wlan.ko"

  install -dm755 "$pkgdir/usr/lib/firmware/qcacld2"
  install -Dm644 usr/lib/firmware/qcacld2/* "$pkgdir/usr/lib/firmware/qcacld2/"

  install -dm755 "$pkgdir/usr/lib/firmware/wlan/qcacld2"
  install -Dm644 usr/lib/firmware/wlan/qcacld2/* "$pkgdir/usr/lib/firmware/wlan/qcacld2/"

  install -Dm644 etc/modprobe.d/reform-qcacld2.conf \
    "$pkgdir/etc/modprobe.d/reform-qcacld2.conf"

  install -Dm644 arch/arm64/boot/Image \
    "$pkgdir/boot/Image-${pkgname}"

  install -Dm644 "imx8mp-mnt-pocket-reform-${pkgver}.dtb" \
    "$pkgdir/boot/imx8mp-mnt-pocket-reform.dtb"

  install -Dm644 "$srcdir/extlinux.conf.example" \
    "$pkgdir/usr/share/doc/${pkgname}/extlinux.conf.example"

  install -Dm644 "$srcdir/mnt-pocket-initramfs.hook" \
    "$pkgdir/usr/share/libalpm/hooks/mnt-pocket-initramfs.hook"

  install -Dm644 "$srcdir/mnt-pocket-backup.hook" \
    "$pkgdir/usr/share/libalpm/hooks/mnt-pocket-backup.hook"

  install -Dm755 "$srcdir/mnt-pocket-backup.sh" \
    "$pkgdir/usr/bin/mnt-pocket-backup.sh"
}

