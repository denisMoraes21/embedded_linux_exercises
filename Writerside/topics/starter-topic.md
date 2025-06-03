# Linux Embarcado

Linux embarcado (ou embedded Linux) é uma versão do sistema operacional Linux adaptada para rodar em dispositivos com 
recursos limitados, como sistemas embarcados. Estes dispositivos geralmente têm menos poder de processamento, menos 
memória e menor capacidade de armazenamento do que computadores tradicionais. É amplamente usado em eletrônicos de
consumo, automação industrial, IoT, roteadores, TVs inteligentes, entre outros.

## Principais Tópicos

### Fundamentos de Linux Embarcado

- Arquitetura do sistema Linux embarcado: bootloader, Kernel, rootfs, aplicação
- Diferença entre Linux full (desktop/server) e Linux embarcado.
- Estudo do sistema de arquivos (/bin, /sbin, /lib, etc).

### Kernel Linux

- Compilação cruzada do kernel (ARCH, CROSS_COMPILE, menuconfig).
- Device Tree (DTB): estrutura, edição e uso.
- Módulos do kernel: criação, carregamento (insmod, modprobe, lsmod).
- Customização do kernel para hardware específico.
- Aplicação de patches no kernel.

### Toolchain e Cross-Compilation

- Compiladores cruzados (arm-linux-gnuabihf-gcc, aarch64-linux-gnu-gcc, etc).
- Configurações e geração de toolchains (crosstool-ng, Linaro, Buildroot).
- Compilação de bibliotecas e aplicações para o alvo (cross-compilation manual).

### Sistemas de build

- Buildroot: criação de rootfs, kernel e toolchain.
- Yocto Project: receitas, camadas, BitBake.
- CMake, Makefile: compilação de projetos embarcados personalizados.

### Root Filesystem e Busybox

- Criação manual de rootfs (com BusyBox).
- Estrutura mínima de um rootfs funcional.
- Sistemas de arquivos: ext2/3/4, squashfs, initramfs, cpio.

### Bootloaders

- U-Boot: configuração, comandos, script de boot (boot.cmd, boot.scr)
- Inicialização de kernel e device tree.
- Atualização de imagens (via TFTP, SD, NAND, etc.).

### Interface e Periféricos

- Comunicação com GPIO, I2C, SPI, UART via sysfs ou /dev.
- Desenvolvimento de drivers simples (character device drivers).
- Configuração de interfaces de rede embarcados (Ethernet, Wi-Fi, PPP, etc).

### Depuração e diagnóstico

- dmesg, strace, gdb, gdbserver, perf, ftrace.
- Monitoramento de uso de CPU/memória em tempo real.
- Console serial para debug de boot e kernel panic.

### Segurança e Atualizações

- Assinatura de kernel e verificações de integridade (Secure Boot, U-Boot SPL).
- Atualizações seguras (OTA): A/B partitions, Mender, SWUpdate, RAUC.
- Minimização da superfície de ataque (redução de serviços e permissões).

### Integrações com aplicações e IOT

- Desenvolvimento de aplicações C/C++ e integração com hardware.
- Comunicação com protocolo como MQTT, Modbus, CAN, etc.
- Monitoramento e controle remoto via rede (SSH, RPC, MQTT).

## Elementos essenciais

- Kernel
- Device Tree
- Root Filesystem
- Bootloader
- Toolchain
- Init System
- Bibliotecas de usuário
- Aplicações de usuário
- Drivers
- Sistemas de arquivos de suporte
- Firmware / Blobs binários
- Configuração do kernel

## Ferramentas comuns

- Toolchains cruzadas
- Build systems
- Bootloaders
- Sistemas de arquivos mínimos
- Depuração

## Referências bibliográficas

