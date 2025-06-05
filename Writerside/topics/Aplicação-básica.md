# Aplicação básica

## Requisitos

- sudo apt update
- sudo apt install build-essential git wget cpio unzip rsync bc python3

## Passos

- git clone https://github.com/buildroot/buildroot.git
- cd buildroot
- make raspberrypi3_defconfig : para raspberypi3, raspberrypi3B, raspberrypi3B+
- make menuconfig
- make
- A imagem irá ficar em: output/images
- sudo dd if=output/images/sdcard.img of=/dev/sda bs=4M status=progress conv=fsync : para gravar no cartão 

OBS: cartão deve estão FAT32

- Resultado: boot (FAT32) com firmware e kernel e rootfs (ext4) com sistema de arquivos raiz.

OBS: o cartão pode acabar não sendo montado, usar: mount | grep /dev/sda

OBS: para desmontar o cartão: sudo unmout /dev/sda

OBS: para funcionar o teclado: 

  - Target packages -> Hardware handling -> usbutils e input-utils
  - Kernel -> Kernel configuration -> Device Drivers -> Input device support (Keyboard interface, Event interface), HID
support (HID bus support, USB HID support), USB support (Support for Host-side USB, EHCI HCD (USB2.0) support, XHCI 
(USB3.0) support, OHCI HCD support)
  - System configuration -> Enable root login with password -> /dev management -> Busybox para eudev
  - Toolchain -> Enable C++ support, Enable threads support, Enable wchar support

- make clean : para limpar a saída

## Configuração Cartão SD

- sudo fdisk /dev/sda

Digite d para deletar partições (se necessário), repita para cada partição.

Digite n para criar uma nova partição primária.

Aceite os valores padrão para usar todo o espaço.

Digite t para mudar o tipo da partição.

Digite b para definir como W95 FAT32.

Digite w para salvar e sair.

- sudo mkfs.vfat -F 32 /dev/sda1 : para formatar