# Instalação do Oracle VirtualBox no Windows

## Introdução

O Oracle VirtualBox é uma plataforma de virtualização que permite executar máquinas virtuais dentro de um computador físico.

Neste documento será apresentada a instalação do Oracle VirtualBox em um computador com Windows. Ao final do procedimento, o VirtualBox estará instalado e pronto para ser utilizado na criação de uma máquina virtual.

A instalação apresentada neste guia utiliza o instalador oficial disponibilizado pela Oracle.

## Pré-requisitos

Antes de iniciar a instalação, é necessário verificar alguns requisitos básicos.

O computador deve possuir:

* Windows compatível com a versão do VirtualBox utilizada
* Processador compatível com a arquitetura da máquina virtual que será utilizada
* Espaço disponível em disco
* Permissão para instalar programas no Windows
* Conexão com a Internet para realizar o download do instalador

Nas versões atuais do VirtualBox 7.2, são disponibilizados pacotes para Windows 10 e Windows 11 em sistemas x86_64. Também existem pacotes específicos para Windows 11 em processadores ARM, com algumas limitações.

Para este laboratório, será considerado um computador Windows com processador x86_64.

## 1. Download do VirtualBox

O instalador deve ser obtido diretamente do site oficial do Oracle VirtualBox.

A página de downloads está disponível em:

https://www.oracle.com/virtualization/technologies/vm/downloads/virtualbox-downloads.html

Na página de downloads, localize a seção correspondente aos pacotes do Oracle VirtualBox.

Para um computador Windows tradicional com processador x86_64, selecione:

```text
Windows Installer
```

O arquivo baixado possui a extensão `.exe`.

O nome do arquivo pode variar de acordo com a versão disponibilizada. Um exemplo seria:

```text
VirtualBox-7.2.16-xxxxx-Win.exe
```

Não é necessário utilizar exatamente esse nome, pois a versão e o número da revisão podem mudar ao longo do tempo.

A Oracle disponibiliza os pacotes de instalação para diferentes sistemas operacionais na página oficial de downloads.

## 2. Iniciando a instalação

Depois de concluir o download, abra a pasta onde o arquivo foi salvo.

Localize o instalador do VirtualBox e execute o arquivo `.exe`.

O Windows poderá apresentar uma solicitação de confirmação para executar o instalador.

Confirme a execução para iniciar o processo de instalação.

Será apresentada a tela inicial do instalador do Oracle VirtualBox.

## 3. Escolhendo os componentes

Na primeira etapa do instalador, o VirtualBox apresenta os componentes que serão instalados.

A instalação padrão inclui os principais componentes necessários para utilizar o VirtualBox.

Entre os componentes disponíveis estão:

* Aplicação principal do VirtualBox
* Suporte a dispositivos USB
* Componentes de rede
* Suporte relacionado à automação e à API do VirtualBox

Os componentes de rede são importantes para que as máquinas virtuais possam utilizar os diferentes modos de conexão de rede oferecidos pelo VirtualBox.

Para uma instalação destinada a estudos, a configuração padrão é suficiente.

Clique em:

```text
Next
```

## 4. Diretório de instalação

O instalador solicitará o diretório onde o VirtualBox será instalado.

Normalmente, não é necessário alterar essa configuração.

A instalação padrão pode ser mantida.

Caso seja necessário utilizar outro local, escolha um diretório adequado e certifique-se de que o Windows permita a instalação nesse caminho.

Para este laboratório, será utilizado o diretório padrão.

Clique em:

```text
Next
```

## 5. Atalhos e registro de arquivos

Durante a instalação, o VirtualBox poderá apresentar opções relacionadas à criação de atalhos e ao registro das extensões de arquivos utilizadas pelo programa.

Entre as extensões associadas ao VirtualBox estão:

```text
.vbox
.vbox-extpack
.ovf
.ova
.vdi
.vmdk
.vhd
.vdd
```

Esses arquivos são utilizados em diferentes situações relacionadas às máquinas virtuais, como configuração, armazenamento de discos virtuais e exportação de appliances.

Para uma instalação comum, as opções padrão podem ser mantidas.

Clique em:

```text
Next
```

## 6. Configuração das interfaces de rede

O instalador também pode informar que serão instalados componentes relacionados à rede.

Isso acontece porque o VirtualBox utiliza drivers específicos para fornecer determinados modos de conectividade às máquinas virtuais.

Durante essa etapa, a conexão de rede do Windows poderá ser temporariamente interrompida.

Isso é esperado durante a instalação dos componentes de rede.

Se o instalador apresentar um aviso informando sobre essa possibilidade, leia a mensagem e prossiga com a instalação.

A documentação oficial do VirtualBox informa que os componentes de rede incluem suporte necessário para funcionalidades como Bridged Networking e Host-only Networking.

## 7. Iniciando a instalação

Depois de revisar as opções selecionadas, o instalador estará pronto para iniciar a instalação.

Clique em:

```text
Install
```

O Windows poderá solicitar novamente autorização para que o instalador faça alterações no computador.

Confirme a operação.

O instalador copiará os arquivos necessários e registrará os componentes do VirtualBox no sistema.

A duração desse processo depende do computador utilizado.

## 8. Drivers do VirtualBox

Durante a instalação, o Windows poderá apresentar solicitações relacionadas à instalação de drivers.

Esses drivers fazem parte do funcionamento do VirtualBox e são necessários para determinados recursos, principalmente aqueles relacionados à virtualização e à rede.

Quando o Windows solicitar autorização para instalar componentes de software da Oracle relacionados ao VirtualBox, verifique a mensagem apresentada e permita a instalação.

A instalação desses componentes é necessária para que o VirtualBox possa funcionar corretamente.

## 9. Finalizando a instalação

Quando a instalação for concluída, o instalador apresentará a tela de conclusão.

Será possível encontrar uma opção para iniciar o VirtualBox imediatamente após o término da instalação.

Caso queira verificar a instalação neste momento, mantenha essa opção selecionada.

Clique em:

```text
Finish
```

O Oracle VirtualBox Manager será iniciado.

## 10. Verificando a instalação

Com o VirtualBox aberto, a janela principal do VirtualBox Manager deverá ser apresentada.

Nesse momento ainda não haverá nenhuma máquina virtual criada.

A ausência de máquinas virtuais é normal, pois a instalação do VirtualBox e a criação de uma máquina virtual são etapas diferentes.

A interface deverá apresentar opções para criar e administrar máquinas virtuais.

Uma instalação concluída corretamente permite utilizar o VirtualBox para criar, configurar, iniciar e administrar máquinas virtuais.

## 11. Verificando pelo terminal

Também é possível verificar a instalação utilizando o Prompt de Comando do Windows.

Abra o:

```text
Prompt de Comando
```

Execute:

```cmd
VBoxManage --version
```

Se o VirtualBox estiver instalado e o comando estiver disponível no `PATH`, será apresentada a versão instalada.

Um resultado semelhante a este poderá ser apresentado:

```text
7.2.16rxxxxx
```

O número apresentado depende da versão instalada.

O `VBoxManage` é uma ferramenta de linha de comando fornecida pelo VirtualBox e permite realizar diversas tarefas de administração das máquinas virtuais.

## 12. Instalação concluída

Neste ponto, o Oracle VirtualBox está instalado no Windows.

O computador utilizado neste laboratório será considerado o sistema hospedeiro, também chamado de host.

O sistema operacional que será instalado posteriormente dentro do VirtualBox será chamado de sistema convidado, ou guest.

A relação pode ser representada da seguinte forma:

```text
Computador físico
       |
       v
     Windows
       |
       v
   VirtualBox
       |
       v
  Máquina Virtual
       |
       v
     Debian
```

O Windows continua sendo o sistema operacional principal do computador.

O Debian será executado dentro de uma máquina virtual criada pelo VirtualBox.

## Próximo passo

Com o VirtualBox instalado, o próximo procedimento será criar uma nova máquina virtual.

Na próxima etapa serão definidos os recursos virtuais da máquina, incluindo:

* Nome da máquina virtual
* Sistema operacional
* Memória RAM
* Processadores
* Disco virtual
* Controladora de armazenamento
* Configuração inicial de rede

O objetivo será preparar uma máquina virtual para a instalação do Debian.

## Referências

Oracle. Oracle VirtualBox Downloads.

https://www.oracle.com/virtualization/technologies/vm/downloads/virtualbox-downloads.html

Oracle. Oracle VirtualBox User Guide 7.2.

https://docs.oracle.com/en/virtualization/virtualbox/7.2/user/

Oracle. Installing Oracle VirtualBox on Windows Hosts.

https://docs.oracle.com/en/virtualization/virtualbox/7.2/user/installation.html

