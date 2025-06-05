# Buildroot

Fonte: https://buildroot.org/downloads/manual/manual.html

Buildroot é uma ferramenta simple, eficiente e fácil de usar para geração de sistemas de linux embarcado através de 
compilação cruzada.
Compilação cruzada de toolchain, geração de root filesystem, compilação de imagem do kernel e compilação do bootloader.
Feito com menuconfig parecido com a interface de configuração kernel, gconfig e xconfig.
Buildroot suporta diversos processadores e suas variações.

Ferramentas de build no buildroot são:
- which
- sed
- make
- binutils
- build-essentials
- gcc
- g++
- bash
- patch
- gzip
- bzip2
- perl
- tar
- cpio
- unzip
- rsync
- file
- bc
- findutils

## Obtendo o buildroot

- curl -O https://buildroot.org/downloads/Vagrantfile; vagrant up

## Quickstart

- make menuconfig

Para menu de configuração original:
- make nconfig

Para usar o nome menu de configuração:
- make xconfig

Para usar o menu de configuração baseado em QT:
- make gconfig

Após a ferramenta gerar o arquivo .config usar o comando "make" para:
- Fazer download de arquivos fonte
- Configurar, buildar e instalar o tooo=lchain de cross compilação;
- Configurar, buildar e instalar os pacotes selecionados.
- Buildar a imagem kernel;
- Buildar a imgem bootloader;
- Criar um sistema de arquivos raíz

A saída estará disponível na pasta "output/":
- images/: onde estão todas as imagens.
- build/: onde estão todos os componentes que foram construídos.
- host/: onde estão todas as ferramentas construídas para o host.
- staging/: symlink que contém o toolchain alvo.
- target/: Contém o filesystem.


