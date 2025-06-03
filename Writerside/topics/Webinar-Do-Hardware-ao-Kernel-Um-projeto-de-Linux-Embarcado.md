# Webinar: Do Hardware ao Kernel: Um projeto de Linux Embarcado

## Como escolher o hardware?

- Arquitetura compatível (x86, ARM, RISCV)
- Suporte ao Linux (documentação, comunidade, fabricante...)
- Interfaces de Comunicação (USB, UART, SPI, Display...)

### Escolhendo o Hardware

- Mesmo não desenvolvendo hardwares, o conhecimento do hardware que se está trabalhando é essencial
- A escolha do hardware define tudo: arquitetura da CPU, periféricos, o tipo de suporte que você terá do fabricante e 
a vida útil que seu produto terá no mercado.

### Arquitetura compatível
 
- Mais usadas: ARM, x86, MIPS, RISC-V
- ARM: possui excelente suporte ao Yocto e ao Buildroot, aplicativos e frameworks pré-compilados para esses dispositivos,
costuma ter baixo consumo de energia, BSPs bem mantidos, etc...
- x86: também possui excelente suporte ao Linux Embarcado, alto processamento, grande compatibilidade para periféricos.
- RISC-V: arquitetura aberta, flexível, porém tem suporte limitado ao Linux (muitos drivers não funcionam, por exemplo), 
rootfs e bootloaders ainda estão em processo de evolução - virou patrocinadora da Yocto Project.
- Interfaces de comunicação: existe toda a pinagem e drives disponíveis para o que o projeto necessita?

### Suporte ao linux

- Boa documentação, comunidade ativa e suporte do fabricante.
- A falta de documentação pode atrasar ou até impossibilitar um projeto: datasheets, esquemáticos, acesso ao device-tree,
detalhes de pinout, entre outros, são essenciais.
- Comunidade ativa e, quanto possível, open source não somente facilitam o processo de desenvolvimento, mas podem trazer
 frameworks prontas e utilizadas, correção de bugs que podem facilitar o seu desenvolvimento, suporte com dúvidas.
- Suporte do fabricante
- Board Support Package (BSP) atualizado
- Existe suporte oficial e abertura ao kernel mainline ou somente um fork do fabricante?
- Long-term Support (LTS)

## Toolchain

- Compilação cruzada
- Compatibilidade com arquitetura
- Footprint e performance
- Tools: Yocto, buildroot, etc...

### Toolchain Introdução

- Conjunto de ferramentas que transformará o código fonte em binários
- Inclui os compiladores (como GCC), binutils (linker e assembler), biblioteca C (glibc, musl, clang), headers do kernel.
- É específico de cada arquitetura
- Determina como vai ser o footprint do binário gerado.
- Ferramenta principal para o processo de compilação cruzada.
- Yocto e buildroot são ferramentas que geram toolchains para a arquitetura que será utilizada

## Kernel

- menuconfig
- Device Tree
- Suporte a drivers do hardware
- Origem: mainline, fork de fabricante

### Kernel Linux

- Responsável por controlar o hardware, gerenciar processos, a memória, os periféricos e os sistemas de arquivos.
- O Kernel não é genérico no Linux Embarcado.
- Ele deve ser configurado para entender o que existe na sua placa e o que deve ser controlado.
- config e menuconfig: mecanismo onde você escolhe o que será habilitado no kernel, ex: drivers, sistemas de arquivos, 
suporte a rede, etc.
- Device Tree: arquivo que descreve o hardware: memória, pinos interfaces como I2C, SPI, etc.
- É através dele que é comunicado para o kernel quais periféricos estão presentes no nosso hardware para que ele possa 
carregar os módulos necessários.
- Drivers: são os códigos específicos para que cada periférico funcione naquele kernel
- Mainline ou Fork: Mainline, oficial do linux, com suporte da comunidade e frequentemente atualizado (ideal). Fork, 
customizado pelo fabricante para o seu hardware, nem sempre atualizado para a utilização do Linux.

## Root Filesystem

- Init system: systemd, init, etc...
- Busybox
- Diretórios (/bin, /dev, etc...)
- Customização (contâiners)

### Rootfs

- O Root Filesystem (RootFS) é o conjunto de arquivos básicos e a arquitetura de pastas que o Linux precisa para funcionar
para depois que o kernel inicializa.
- O que esperar dentro do rootfs: /bin - comandos básicos (ex: ls, cp, sh), /etc - configurações do sistema, /dev - dis-
positivos conectados, /proc e /sys - informações do kernel e hardware, /lib - bibliotecas usadas pelos programas.
- Sistema de init: é o primeiro processo iniciado pelo kernel. Exemplo são systemd, init, runinit, OpenRC.
- BusyBox: Um conjunto de comandos compactados em um único binário. Ideal para sistemas minimalistas com pouco espaço 
como no caso de Sistemas Embarcados.
- Aplicações e customizações: Scripts próprios, aplicativos embarcados, atualizações OTA, e até contâiners com aplicações
isoladas (ex: com docker ou podman).

## Console e Boot

- Bootloader (Uboot, etc...)
- Parâmetros do boot
- Debug e troubleshooting do sistema

### Console e Demo

- Abordagem monolítica: Imagem simples e bootável (core-image-minimal), gerada pelo Yocto Project. Possui os componentes
básicos como u-boot, kernel, módulos e Busybox.
- Abordagem via containers: Imagem com sistema Pantavisor para gerenciamento de containers. As aplicações são instaladas 
de forma separada e isoladas através de containers LXC. Contém u-boot, kernel, módulos, gerenciador de containers (Panta
visor) e containers.




