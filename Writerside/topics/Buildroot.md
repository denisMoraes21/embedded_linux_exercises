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
- Configurar, buildar e instalar o toolchain de cross compilação;
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

## Configuração do build

Para pedir ajuda:
- no menuconfig é "/"
- no xconfig é "Ctrl + f"

Existe a cross-compilation toolchain e a host-compilation toolchain, interna e externa respectivamente.
Na interna é possível mudar a versão do Kernel, mudar versão de GCC, compiler, binutils e a lib C, como também ativar
outras extensões para usar outras ferramentas.
No externo é possível recompilar algum build já existente, poupando tempo. É possivel usar um perfil de toolchain 
externa pré definida e deixar o Buildroot baixar, extrair e instalar a toolchain; é possível usar um perfil de toolchain
externa pré definida e dizer ao Buildroot onde a sua toolchain está instalada em seu computador; e é possível usar uma
toolchain externa totalmente customizada.
Buildroot não consegue usar toolchain de outras ferramentas como OpenEmbedded e Yocto pois suas pré-compilações são muito
pesadas.

## /dev management

Pasta onde estão os drivers do sistema.
Buildroot tem 4 abordagens para manipulação:
- Tabela estática de dispostivos utilizados (system/device_table_dev.txt), versão clássica do Linux.
- Dinâmica usando devtmpfs apenas (Linux 2.6.32), Device virtual, aparece e desaparece do sistema quando dispositivo
conectado.
- Dinâmica usando devtmpfs + mdev, quando conectado fica acessível ao espaço de usuário para fazer implementações.
- Dinâmica usando devtmpfs + eudev, quando conectado fica acessível ao espaço de daemon para fazer implementações.

## init system

É o primeiro programa a iniciar, buildroot deixa utilizar três tipos:
- BusyBox: lê o /etc/inittab para saber o que fazer primeiro. O resultado fica no package/busybox/initab
- SystemV: Muito utilizado mas já sendo substituido por Upstart e Systemd.
- Systemd: Capacidade de paralelização, socket e D-bus para ativar serviços, iniciar daemons sob demanda

# Uso genérico do buildroot

- make V=1 target = mostra todos os comandos que podem ser executados por make.
- make list-defconfigs - mostra uma lista de placas com defconfig.
- make help - mostra todos os targets disponíveis (busybox-menuconfig, linux-menuconfig, uclibc-menuconfig, barebox-
menuconfig, uboot-menuconfig)
- make clean - somente necessário quando mudar arquitetura ou toolchain.
- make manual-clean - limpa manual.
- make manual - compila manual.
- make distclean - limpa todos os resultado do build.
- make clean all - limpa tudo.

## Entendendo quando um rebuild é necessário

- É responsabilidade saber o que deve ser reconstruído.
- Quando a configuração da arquitetura é alterada, é necessário rebuildar tudo.
- Quando a configuração da toolchain é alterada, é necessário rebuildar tudo.
- Quando um pacote é adicionado, não é necessário rebuildar tudo.
- Quando um pacote é removido, não é necessário fazer nada.
- Quando alterações nos pacotes são feitas, é necessário rebuild apenas para os pacotes.
- Quando o esqueleto do root filesystem é mudado, um rebuild completo é necessário.

## Entendendo como rebuildar pacotes.

- make pacote-dirclean : limpa o diretório de saída.
- make pacote-rebuild : reiniciar o processo de compilação.
- make source: para baixar todas as dependências necessárias.
- make O=/tmp/build menuconfig : para compilar coisas fora da pasta principal

## Variáveis de ambiente

- HOSTCXX: especificar versão do compilador de C++
- HOSTCC: especificar versão do compilador de C.
- UCLIBC_CONFIG_FILE: especificar toolchain
- BUSYBOX_CONFIG_FILE: especificar versão do busybox
- BR2_CCACHE_DIR: para especificar onde o Buildroot guarda o cache.
- BR2_DL_DIR: para especificar onde serão guardados os downloads.
- BR2_GRAPH_ALT: especificar esquema de cores alternativo para gráficos.
- BR2_GRAPH_OUT: especificar o tipo de arquivo de geração de gráficos.
- BR2_GRAPH_DEPS_OPTS: passar dependências extras para o gráfico de dependência.
- BR2_GRAPH_DOT_OPTS: dependências gráficas.
- BR2_GRAPH_SIZE_OPTS: tamanho do gráfico.

OBS: utilizar arquivos esparsos é permitido, mas pode gerar erro de compilação corrompendo o sistema.

- make show-info: json com informações sobre pacotes.
- make pckg-stats: para saber se tem versão superior.

É possível gerar gráficos entre dependências de pacotes.
É possível gerar gráficos de duração de build.
É possível gerar gráficos de tamanho de sistema de arquivos.

Build paralelo: Pode usar make -jN ou alterar BR2_JLEVEL ou habilitar BR2_PER_PACKAGE_DIRECTORIES

 