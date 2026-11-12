# Configurando Pastas Compartilhadas entre Windows e Debian

## Introdução

Após instalar o Debian e configurar a conectividade de rede, podemos configurar uma pasta compartilhada entre o Windows e a máquina virtual.

O Oracle VirtualBox possui o recurso **Shared Folders**, que permite disponibilizar um diretório existente no sistema hospedeiro para ser acessado pelo sistema convidado.

Neste laboratório, o Windows será o sistema hospedeiro e o Debian será o sistema convidado.

O recurso será utilizado para facilitar a transferência de arquivos entre os dois sistemas.

Para utilizar pastas compartilhadas em uma máquina virtual Linux, é necessário instalar as **Oracle VirtualBox Guest Additions** no sistema convidado.

## Objetivo

Ao final deste procedimento, teremos uma pasta criada no Windows e disponibilizada para o Debian por meio do recurso de pastas compartilhadas do Oracle VirtualBox.

A estrutura do ambiente será:

```text
Windows
    |
    +-- Pasta compartilhada
           |
           v
    Oracle VirtualBox
           |
           v
        Debian
           |
           +-- Pasta montada
```

## Pré-requisitos

Antes de iniciar, é necessário ter:

* Oracle VirtualBox instalado no Windows
* Máquina virtual `debian-lab` criada
* Debian instalado
* Máquina virtual funcionando corretamente
* Usuário com privilégios administrativos no Debian

A instalação do Debian é apresentada no documento:

```text
docs/windows/04-instalando-o-debian.md
```

A configuração de rede é apresentada no documento:

```text
docs/windows/05-configurando-a-rede.md
```

## Entendendo as pastas compartilhadas

Uma pasta compartilhada pertence fisicamente ao sistema hospedeiro.

Neste laboratório, a pasta será criada no Windows e disponibilizada para o Debian por meio do VirtualBox.

O Debian não acessará essa pasta como um diretório comum do Windows. O VirtualBox disponibilizará o diretório utilizando seu mecanismo de pastas compartilhadas.

A estrutura pode ser representada da seguinte forma:

```text
Sistema hospedeiro
Windows
    |
    +-- C:\VirtualBox\Shared
              |
              v
       Oracle VirtualBox
              |
              v
        Máquina virtual
              |
              v
           Debian
              |
              +-- /mnt/shared
```

## Instalando as Guest Additions

As Guest Additions são componentes instalados dentro da máquina virtual.

Além das pastas compartilhadas, elas fornecem recursos adicionais para melhorar a integração entre o sistema hospedeiro e o sistema convidado.

A imagem das Guest Additions é disponibilizada junto com o Oracle VirtualBox e pode ser inserida na máquina virtual pelo menu **Devices**.

## Verificando a versão do VirtualBox

Antes de instalar as Guest Additions, é recomendável verificar a versão do VirtualBox utilizada no computador hospedeiro.

No Windows, abra o Prompt de Comando e execute:

```cmd
VBoxManage --version
```

Um resultado semelhante poderá ser apresentado:

```text
7.2.16rxxxxx
```

A versão exata depende da versão instalada no computador.

## Inserindo a imagem das Guest Additions

Inicie a máquina virtual `debian-lab`.

Com o Debian em execução, no menu do VirtualBox selecione:

```text
Devices
    |
    +-- Insert Guest Additions CD Image
```

O VirtualBox disponibilizará a imagem `VBoxGuestAdditions.iso` para a máquina virtual.

A imagem será apresentada ao Debian como uma unidade óptica virtual.

## Verificando a mídia no Debian

Após inserir a imagem, o Debian poderá reconhecer automaticamente a unidade óptica.

Também é possível verificar os dispositivos disponíveis utilizando:

```bash
lsblk
```

Um dispositivo de mídia óptica poderá aparecer na listagem.

O resultado exato depende da configuração da máquina virtual.

## Preparando o Debian

Para instalar as Guest Additions no Debian, alguns pacotes necessários ao processo de instalação podem ser necessários.

Atualize a lista de pacotes:

```bash
sudo apt update
```

Em seguida, instale os componentes necessários para compilar os módulos utilizados pelas Guest Additions:

```bash
sudo apt install build-essential dkms linux-headers-$(uname -r)
```

O pacote `linux-headers` deve corresponder ao kernel em execução.

A versão do kernel pode ser consultada utilizando:

```bash
uname -r
```

## Acessando a mídia das Guest Additions

Depois de inserir a imagem, verifique se o sistema reconheceu a mídia.

Um dispositivo de CD/DVD poderá estar disponível em um diretório como:

```text
/media/cdrom
```

ou em outro ponto de montagem definido pelo sistema.

Para verificar os dispositivos montados, utilize:

```bash
mount
```

Também é possível verificar os dispositivos de bloco utilizando:

```bash
lsblk
```

O local exato poderá variar de acordo com o ambiente gráfico e a configuração do Debian.

## Instalando as Guest Additions

Depois de localizar a mídia, execute o instalador fornecido pelas Guest Additions.

Em uma situação em que a mídia esteja montada em `/media/cdrom`, o instalador poderá ser executado utilizando:

```bash
sudo sh /media/cdrom/VBoxLinuxAdditions.run
```

O instalador realizará as etapas necessárias para adicionar os componentes ao sistema.

A saída apresentada durante o processo pode variar de acordo com a versão do VirtualBox e do Debian.

## Reiniciando o Debian

Após a instalação das Guest Additions, reinicie a máquina virtual:

```bash
sudo reboot
```

O reinício é necessário para que os componentes instalados sejam carregados corretamente.

## Verificando as Guest Additions

Após o reinício, é possível verificar se os módulos relacionados às Guest Additions estão carregados.

Utilize:

```bash
lsmod | grep vbox
```

Dependendo da versão instalada e dos componentes utilizados, poderão aparecer módulos relacionados ao VirtualBox.

## Criando a pasta no Windows

Com as Guest Additions instaladas, crie no Windows o diretório que será compartilhado.

Neste laboratório será utilizado:

```text
C:\VirtualBox\Shared
```

O nome e o local da pasta podem ser diferentes.

Dentro desse diretório, crie um arquivo de teste:

```text
C:\VirtualBox\Shared\teste.txt
```

O arquivo será utilizado posteriormente para verificar se o Debian consegue acessar o conteúdo da pasta.

## Configurando a pasta compartilhada no VirtualBox

Com a máquina virtual desligada ou em execução, o VirtualBox permite configurar pastas compartilhadas.

No VirtualBox Manager, selecione:

```text
debian-lab
    |
    +-- Configurações
           |
           +-- Pastas Compartilhadas
```

Adicione uma nova pasta compartilhada.

Para este laboratório, utilize:

```text
Caminho da pasta: C:\VirtualBox\Shared
Nome do compartilhamento: shared
```

A opção de montagem automática poderá ser utilizada para facilitar o acesso à pasta.

Uma configuração possível será:

```text
Pasta do Windows: C:\VirtualBox\Shared
Nome: shared
Somente leitura: desabilitado
Montagem automática: habilitada
```

A opção de somente leitura deve permanecer desabilitada caso seja necessário criar, alterar ou remover arquivos a partir do Debian.

## Nome do compartilhamento

O nome configurado no VirtualBox é diferente do caminho físico da pasta no Windows.

Neste laboratório:

```text
Caminho físico:
C:\VirtualBox\Shared

Nome do compartilhamento:
shared
```

O Debian utilizará o nome `shared` para identificar o compartilhamento.

## Verificando o compartilhamento no Debian

Depois de configurar a pasta, inicialize ou reinicie a máquina virtual caso necessário.

Quando a montagem automática estiver habilitada, o VirtualBox poderá montar a pasta automaticamente no Debian.

Em sistemas Linux, pastas compartilhadas montadas automaticamente pelo VirtualBox normalmente ficam disponíveis abaixo de:

```text
/media
```

O nome poderá seguir o padrão:

```text
/media/sf_shared
```

O prefixo `sf_` é utilizado pelo VirtualBox para identificar compartilhamentos montados automaticamente.

## Verificando a pasta montada

Para verificar se o compartilhamento está disponível, utilize:

```bash
ls -la /media
```

Caso o compartilhamento esteja montado automaticamente, poderá aparecer:

```text
sf_shared
```

Também é possível consultar diretamente:

```bash
ls -la /media/sf_shared
```

O arquivo criado anteriormente no Windows deverá aparecer na listagem:

```text
teste.txt
```

## Montando manualmente a pasta

Também é possível montar a pasta compartilhada manualmente.

Primeiro, crie um ponto de montagem:

```bash
sudo mkdir -p /mnt/shared
```

Depois, monte o compartilhamento:

```bash
sudo mount -t vboxsf shared /mnt/shared
```

Nesse comando:

```text
shared
```

é o nome definido no VirtualBox.

E:

```text
/mnt/shared
```

é o diretório utilizado como ponto de montagem no Debian.

## Verificando a montagem

Depois de realizar a montagem manual, verifique o conteúdo:

```bash
ls -la /mnt/shared
```

O arquivo criado no Windows deverá aparecer:

```text
teste.txt
```

Também é possível verificar os sistemas de arquivos montados:

```bash
mount | grep vboxsf
```

Um resultado semelhante poderá ser apresentado:

```text
shared on /mnt/shared type vboxsf
```

As informações exatas podem variar de acordo com a configuração do sistema.

## Testando a escrita pelo Debian

Para confirmar que o compartilhamento permite gravação, crie um arquivo dentro da pasta montada:

```bash
touch /mnt/shared/teste-debian.txt
```

Verifique o arquivo:

```bash
ls -la /mnt/shared
```

O arquivo deverá aparecer na listagem.

Agora verifique a pasta no Windows.

O arquivo:

```text
teste-debian.txt
```

deverá estar disponível em:

```text
C:\VirtualBox\Shared
```

Esse teste confirma que o Debian conseguiu gravar um arquivo no diretório compartilhado.

## Testando a escrita pelo Windows

Também podemos realizar o teste no sentido contrário.

No Windows, crie um novo arquivo dentro de:

```text
C:\VirtualBox\Shared
```

Por exemplo:

```text
windows.txt
```

Depois, no Debian, execute:

```bash
ls -la /mnt/shared
```

O arquivo deverá aparecer:

```text
windows.txt
```

Dessa forma, podemos confirmar a comunicação de arquivos entre os dois sistemas.

## Permissões do compartilhamento

As pastas compartilhadas do VirtualBox possuem algumas particularidades relacionadas às permissões no Linux.

Quando uma pasta compartilhada é montada automaticamente, o acesso normalmente é controlado pelo grupo:

```text
vboxsf
```

O usuário que precisa acessar a pasta deve fazer parte desse grupo.

## Verificando o grupo vboxsf

Para verificar se o grupo existe, utilize:

```bash
getent group vboxsf
```

Um resultado semelhante poderá ser:

```text
vboxsf:x:999:
```

O número do grupo pode variar.

## Adicionando o usuário ao grupo vboxsf

Caso o usuário ainda não pertença ao grupo `vboxsf`, adicione-o utilizando:

```bash
sudo usermod -aG vboxsf $USER
```

Depois disso, é necessário encerrar a sessão e entrar novamente ou reiniciar o Debian para que a nova associação de grupo seja aplicada.

Uma forma simples de reiniciar é:

```bash
sudo reboot
```

## Verificando os grupos do usuário

Após entrar novamente no sistema, verifique os grupos do usuário:

```bash
groups
```

O grupo:

```text
vboxsf
```

deverá aparecer na listagem.

## Testando novamente o acesso

Depois de confirmar que o usuário pertence ao grupo `vboxsf`, tente acessar novamente o compartilhamento:

```bash
ls -la /mnt/shared
```

Caso a montagem automática esteja sendo utilizada:

```bash
ls -la /media/sf_shared
```

O usuário deverá conseguir acessar os arquivos conforme as permissões configuradas para o compartilhamento.

## Desmontando a pasta

Quando uma pasta tiver sido montada manualmente, ela poderá ser desmontada utilizando:

```bash
sudo umount /mnt/shared
```

Depois disso, o diretório continuará existindo, mas não estará mais associado ao compartilhamento.

Para verificar:

```bash
mount | grep vboxsf
```

Se nenhum resultado for apresentado, o compartilhamento manual não estará montado naquele momento.

## Montagem automática

O VirtualBox também permite configurar uma pasta compartilhada para ser montada automaticamente.

Quando essa opção é utilizada, o Guest Additions realiza a montagem durante a inicialização do sistema convidado.

No Linux, um compartilhamento configurado dessa maneira poderá aparecer em um caminho semelhante a:

```text
/media/sf_shared
```

O caminho pode variar de acordo com as configurações do VirtualBox e do sistema convidado.

## Configuração utilizada

A configuração utilizada neste laboratório será:

| Recurso                  | Configuração           |
| ------------------------ | ---------------------- |
| Sistema hospedeiro       | Windows                |
| Sistema convidado        | Debian                 |
| Máquina virtual          | `debian-lab`           |
| Pasta no Windows         | `C:\VirtualBox\Shared` |
| Nome do compartilhamento | `shared`               |
| Modo                     | Leitura e escrita      |
| Guest Additions          | Instaladas             |
| Grupo Linux              | `vboxsf`               |
| Ponto de montagem manual | `/mnt/shared`          |

## Resultado

Após concluir este procedimento, teremos uma pasta compartilhada entre o Windows e o Debian.

A estrutura do laboratório será:

```text
Windows
    |
    +-- C:\VirtualBox\Shared
    |       |
    |       +-- teste.txt
    |       +-- teste-debian.txt
    |
    v
Oracle VirtualBox
    |
    v
debian-lab
    |
    +-- Debian
           |
           +-- /mnt/shared
                  |
                  +-- teste.txt
                  +-- teste-debian.txt
```

Os arquivos poderão ser transferidos entre o Windows e o Debian utilizando o diretório compartilhado.

## Considerações finais

As pastas compartilhadas são um recurso útil para laboratórios de virtualização, principalmente quando é necessário transferir arquivos entre o sistema hospedeiro e o sistema convidado.

Neste laboratório foi configurada uma pasta localizada no Windows e disponibilizada para o Debian por meio do recurso **Shared Folders** do Oracle VirtualBox.

Também foram instaladas as Guest Additions, configurado o compartilhamento e realizados testes de leitura e escrita.

O acesso ao compartilhamento no Linux também foi relacionado ao grupo `vboxsf`, utilizado pelo VirtualBox para controlar o acesso às pastas compartilhadas.

Para ambientes de laboratório, esse recurso pode facilitar tarefas como transferência de scripts, arquivos de configuração, códigos-fonte e outros arquivos utilizados durante os estudos.

## Próxima etapa

Com a máquina virtual configurada, com rede funcional e com uma forma prática de compartilhar arquivos entre o Windows e o Debian, o próximo procedimento será trabalhar com snapshots.

Os snapshots permitirão registrar o estado da máquina virtual em determinado momento e posteriormente retornar a esse estado quando necessário.

O procedimento será documentado em:

```text
docs/windows/07-snapshots.md
```

