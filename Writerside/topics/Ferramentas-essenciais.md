# Ferramentas essenciais

## Toolchains cruzadas

É um conjunto de ferramentas de compilação que permite você compilar programas em um computador para que rodem em um
sistema com outra arquitetura.
    
- GCC (cross-compiler): compilador principal (ex: arm-none-eabi-gcc, aarch64-linux-gnu-gcc)
- Binutils: ferramentas como as (assembler) e ld (linker).
- Libc: biblioteca C (ex: glibc, musl, uClibc).
- Headers do kernel: para compilar drivers e aplicativos nativos
- Debugger: gdb para arquitetura alvo (cross-gdb).


## Build systems: 

- Yocto
- Buildroot
- OpenEmbedded

## Bootloaders: 

- U-Boot
- Barebox

## Sistemas de arquivos mínimos

- BusyBox
- SquashFS

## Depuração

- GDB
- JTAG
- serial console
- OpenOCD
