# KonomiTV環境構築

### 環境

* Ubuntu 24.04 LTS (CHUWI HeroBox, Intel N100, 8GB RAM)
* PLEX PX-W3U4


### ライブラリの準備

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install -y ffmpeg build-essential cmake g++ git libpcsclite-dev nodejs npm lshw curl pkg-config automake autoconf
```

### Docker インストール

https://docs.docker.com/engine/install/ubuntu/


### PLEXチューナーのドライバのセットアップ

```bash
git clone https://github.com/tsukumijima/px4_drv
cd px4_drv/fwtool
make
wget http://plex-net.co.jp/plex/pxw3u4/pxw3u4_BDA_ver1x64.zip 
unzip -oj pxw3u4_BDA_ver1x64.zip pxw3u4_BDA_ver1x64/PXW3U4.sys
/fwtool PXW3U4.sys it930x-firmware.bin
sudo mkdir -p /lib/firmware
sudo cp it930x-firmware.bin /lib/firmware/

# ドライバインストール
wget https://github.com/tsukumijima/px4_drv/releases/download/v0.4.4/px4-drv-dkms_0.4.4_all.deb
sudo apt install -y ./px4-drv-dkms_0.4.4_all.deb

# カーネルモジュール確認
sudo modprobe px4_drv
lsmod | grep -e ^px4_drv
# ↑でpx4_drvが出てきたらOK

# デバイスを繋いだ状態で↓を打って何か出てくればOK
# W3U4なら BS/BS/地デジ/地デジ の順
ls /dev/px*
```


### SoftCasのセットアップ

URLは自宅サーバ（Cloudflare Tunnel）の一時的なもの。ファイル転送がめんどくさかったので…。

```bash
wget https://shared.anseketa.men/temp.softcas.zip
unzip softcas.zip
cd softcas
make
sudo cp libpcsclite.so.1.0.0 /usr/lib/x86_64-linux-gnu/libpcsclite2.so
sudo cp /usr/lib/x86_64-linux-gnu/pkgconfig/libpcsclite.pc /usr/lib/x86_64-linux-gnu/pkgconfig/libpcsclite2.pc
sudo nano /usr/lib/x86_64-linux-gnu/pkgconfig/libpcsclite2.pc
# Libs: の行の lpcsclite を lpcsclite2 にする
```

```bash
wget https://shared.anseketa.men/temp/pt1.zip
unzip pt1.zip
cd pt1/arib25/
nano src/Makefile
# libpcsclite を libpcsclite2 に置き換える（2箇所）
make
sudo make install

cd ~
wget https://shared.anseketa.men/temp/pt1-recpt1.zip
unzip pt1-recpt1.zip
cd pt1-recpt1/recpt1
sed -i 's/pt1video/px4video/g' pt1_dev.h

./autogen.sh
./configure --enable-b25
make
sudo make install
```


### Mirakurunのセットアップ

```bash
sudo npm install -g pm2
sudo npm install mirakurun -g --unsafe-perm --foreground-scripts --production
```


### エンコーダ（Intel QSV）のセットアップ

```bash
mkdir ~/KonomiTV
cd ~/KonomiTV
curl -fsSL https://repositories.intel.com/graphics/intel-graphics.key | sudo gpg --dearmor --yes -o /usr/share/keyrings/intel-graphics-keyring.gpg
echo 'deb [arch=amd64 signed-by=/usr/share/keyrings/intel-graphics-keyring.gpg] https://repositories.intel.com/graphics/ubuntu jammy arc' | sudo tee /etc/apt/sources.list.d/intel-graphics.list > /dev/null
sudo apt update && sudo apt install -y intel-media-va-driver-non-free intel-opencl-icd libmfxgen1
```


### KonomiTVのセットアップ

```
curl -LO https://github.com/tsukumijima/KonomiTV/releases/download/v0.10.1/KonomiTV-Installer.elf
chmod a+x KonomiTV-Installer.elf
sudo ./KonomiTV-Installer.elf
```
