# Instalando o Debian em uma Máquina Virtual

## Introdução

Após criar e configurar a máquina virtual no Oracle VirtualBox, o próximo passo é instalar o sistema operacional que será utilizado no ambiente de laboratório.

Neste documento será realizada a instalação do Debian dentro da máquina virtual `debian-lab`.

O processo será realizado utilizando a imagem ISO do Debian associada à unidade óptica virtual da máquina.

Ao final deste procedimento, o Debian estará instalado no disco virtual e a máquina estará pronta para o primeiro acesso ao sistema.

## Objetivo

Ao final deste procedimento, teremos o Debian instalado e inicializado dentro da máquina virtual criada anteriormente.

A estrutura do ambiente será:

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
  debian-lab
       |
       v
     Debian
```

## Pré-requisitos

Antes de iniciar a instalação, é necessário ter:

* Oracle VirtualBox instalado no Windows
* Máquina virtual `debian-lab` criada
* Máquina virtual configurada
* Imagem ISO do Debian
* Disco virtual disponível para instalação

A criação da máquina virtual é apresentada no documento:

```text
docs/windows/02-criando-a-maquina-virtual.md
```

A configuração da máquina virtual é apresentada no documento:

```text
docs/windows/03-configurando-a-maquina-virtual.md
```

## Iniciando a máquina virtual

Abra o Oracle VirtualBox.

Na tela principal do VirtualBox Manager, selecione a máquina virtual:

```text
debian-lab
```

Com a máquina selecionada, clique em:

```text
Start
```

O VirtualBox iniciará a máquina virtual.

Como a imagem ISO do Debian está associada à unidade óptica virtual, a máquina poderá inicializar utilizando essa mídia.

## Inicialização pela imagem ISO

Durante a inicialização, o VirtualBox apresentará a tela de boot do instalador do Debian.

A aparência dessa tela pode variar de acordo com a versão da imagem utilizada.

Entre as opções disponíveis normalmente estarão opções relacionadas à instalação e inicialização do Debian.

Para iniciar a instalação, selecione a opção de instalação desejada.

Uma instalação utilizando interface gráfica pode ser iniciada pela opção:

```text
Graphical Install
```

Também é possível utilizar a instalação em modo texto por meio da opção:

```text
Install
```

Para este laboratório será utilizada a opção:

```text
Graphical Install
```

## Selecionando o idioma

O instalador solicitará a seleção do idioma utilizado durante o processo de instalação.

Selecione o idioma desejado.

Neste laboratório será utilizado:

```text
Português do Brasil
```

O idioma escolhido será utilizado nas telas do instalador e poderá influenciar algumas configurações regionais do sistema.

## Selecionando a localização

Em seguida, o instalador solicitará a localização do computador.

Selecione:

```text
Brasil
```

Essa configuração será utilizada pelo Debian para definir informações relacionadas à localização e às configurações regionais.

## Configurando o teclado

O instalador solicitará a configuração do layout do teclado.

Para um teclado utilizado no Brasil, selecione uma configuração compatível com o padrão utilizado no computador.

Neste laboratório será utilizado:

```text
Português Brasileiro
```

A configuração correta do teclado é importante para que caracteres especiais e teclas específicas funcionem corretamente dentro do sistema.

## Configurando a rede

Durante a instalação, o Debian poderá tentar configurar automaticamente uma interface de rede.

A máquina virtual utiliza o adaptador de rede configurado no VirtualBox.

Neste laboratório, a máquina está utilizando:

```text
Adaptador 1: habilitado
Modo de conexão: NAT
```

O funcionamento e a configuração da rede serão abordados de forma detalhada posteriormente no documento:

```text
docs/windows/05-configurando-a-rede.md
```

Neste momento, o objetivo é apenas permitir que a instalação prossiga.

## Definindo o nome da máquina

O instalador solicitará um nome para identificar o computador na rede.

Para este laboratório será utilizado:

```text
debian-lab
```

Esse nome será utilizado pelo sistema para identificar a máquina.

## Configurando o domínio

O instalador poderá solicitar um domínio de rede.

Em um laboratório local que não utiliza um domínio específico, esse campo pode permanecer vazio.

Para este laboratório:

```text
Domínio: deixar em branco
```

A configuração de domínio poderá ser realizada posteriormente caso o ambiente passe a utilizar uma infraestrutura de rede que necessite desse recurso.

## Configurando a senha do usuário root

Dependendo da versão e do fluxo de instalação utilizado, o instalador poderá apresentar uma etapa relacionada à conta `root`.

O `root` é o usuário administrativo do sistema Linux e possui privilégios elevados.

Caso o instalador solicite uma senha para o `root`, utilize uma senha adequada para o ambiente de laboratório.

Exemplo:

```text
Usuário: root
Senha: definida durante a instalação
```

A senha utilizada no laboratório deve ser armazenada de forma segura e não deve ser publicada na documentação.

## Criando o usuário

O instalador solicitará informações para criação do usuário que será utilizado no sistema.

Informe o nome da pessoa ou identificação desejada.

Por exemplo:

```text
Nome completo: Usuario Linux
```

Em seguida, será solicitado o nome de usuário.

Neste laboratório será utilizado como exemplo:

```text
Usuário: linux
```

O nome de usuário será utilizado posteriormente para acessar o sistema.

## Definindo a senha do usuário

Defina uma senha para o usuário criado.

Exemplo:

```text
Usuário: linux
Senha: definida durante a instalação
```

A senha deve ser mantida em segurança.

Não utilize senhas reais ou informações pessoais nos exemplos publicados neste repositório.

## Configurando o particionamento

O instalador do Debian solicitará a definição do particionamento do disco.

Neste laboratório será utilizado o disco virtual de:

```text
20 GB
```

Para uma instalação simples em uma máquina virtual de laboratório, o particionamento automático é suficiente.

Selecione a opção de particionamento guiado.

Uma configuração simples pode utilizar:

```text
Particionamento guiado
```

O instalador apresentará o disco virtual disponível para instalação.

Selecione o disco criado anteriormente para a máquina `debian-lab`.

## Esquema de particionamento

O Debian poderá apresentar diferentes opções de particionamento.

Para este laboratório será utilizado um esquema simples, adequado para uma máquina virtual destinada a estudos.

A estrutura final poderá ser semelhante a:

```text
Disco virtual
    |
    +-- Partição do sistema
    |
    +-- Área de swap
```

O layout exato poderá variar de acordo com a versão do instalador e as opções selecionadas durante a instalação.

## Confirmando o particionamento

Antes de aplicar as alterações, o instalador apresentará um resumo do particionamento.

Revise as informações apresentadas.

O disco utilizado neste laboratório será:

```text
Disco virtual: 20 GB
```

Depois de confirmar que o disco correto foi selecionado, escolha a opção para finalizar o particionamento e gravar as alterações no disco.

O instalador solicitará uma confirmação antes de realizar as alterações.

Confirme a operação.

## Instalando o sistema básico

Após confirmar o particionamento, o instalador começará a copiar os arquivos necessários para o disco virtual.

Durante essa etapa serão instalados os componentes básicos do Debian.

O tempo necessário depende do desempenho do computador físico e dos recursos disponibilizados para a máquina virtual.

Durante o processo, aguarde a conclusão da instalação.

## Configurando o gerenciador de pacotes

O instalador poderá solicitar informações relacionadas aos repositórios de pacotes utilizados pelo Debian.

Os repositórios permitem que o sistema obtenha pacotes e atualizações posteriormente.

Caso seja solicitado um servidor de espelho, selecione um repositório apropriado para a localização do laboratório.

Para um ambiente localizado no Brasil, pode ser utilizado um mirror disponível para a região.

A configuração exata poderá variar de acordo com a versão do Debian e os mirrors disponíveis no momento da instalação.

## Configurando o uso de um proxy

O instalador poderá solicitar informações sobre um servidor proxy HTTP.

Caso a rede utilizada pelo laboratório não possua um proxy, deixe o campo vazio.

Para este laboratório:

```text
Proxy HTTP: nenhum
```

A configuração de proxy poderá ser realizada posteriormente caso seja necessária.

## Selecionando os programas

O instalador apresentará opções relacionadas aos componentes de software que serão instalados.

A seleção depende da finalidade da máquina.

Como este ambiente será utilizado para estudos de Linux, infraestrutura e DevOps, uma instalação com os componentes necessários para um ambiente básico é suficiente.

Dependendo da imagem e da versão utilizada, poderão aparecer opções como:

```text
Ambiente de desktop
Servidor SSH
Utilitários padrão do sistema
```

Para este laboratório, o ambiente de desktop pode ser instalado para facilitar a utilização inicial da máquina virtual.

O servidor SSH poderá ser habilitado caso seja desejado realizar posteriormente acessos remotos à máquina.

A seleção dos componentes pode ser modificada posteriormente utilizando o gerenciador de pacotes do Debian.

## Instalando o carregador de inicialização

Durante a instalação, o Debian poderá solicitar a instalação do carregador de inicialização GRUB.

O GRUB é responsável por iniciar o sistema operacional durante o processo de boot.

Para esta máquina virtual, permita a instalação do GRUB.

Quando solicitado o dispositivo de instalação, selecione o disco virtual utilizado pela máquina.

Exemplo:

```text
Disco virtual da máquina
```

O dispositivo exato apresentado pelo instalador pode variar de acordo com a configuração da máquina virtual.

## Finalizando a instalação

Depois da instalação dos componentes e do carregador de inicialização, o instalador realizará as etapas finais de configuração.

Ao concluir, será apresentada uma mensagem informando que a instalação foi finalizada.

O instalador poderá solicitar a remoção da mídia de instalação.

Como a instalação foi realizada utilizando uma imagem ISO, será necessário garantir que a máquina não continue inicializando pelo instalador.

Caso seja solicitado, remova a mídia de instalação virtual ou permita que o VirtualBox reinicie a máquina utilizando o disco virtual.

## Reiniciando a máquina virtual

Após concluir a instalação, reinicie a máquina virtual.

O Debian deverá ser inicializado a partir do disco virtual criado anteriormente.

A sequência será:

```text
VirtualBox
    |
    v
debian-lab
    |
    v
Disco virtual
    |
    v
GRUB
    |
    v
Debian
```

Se a instalação tiver sido concluída corretamente, o sistema operacional será carregado.

## Primeiro acesso

Após a inicialização, será apresentada a tela de login do Debian, caso um ambiente gráfico tenha sido instalado.

Utilize o usuário criado durante a instalação.

Exemplo:

```text
Usuário: linux
Senha: definida durante a instalação
```

Após autenticar, o usuário terá acesso ao ambiente Debian.

## Verificando o sistema

Depois de acessar o Debian, abra um terminal para verificar algumas informações básicas do sistema.

Execute:

```bash
cat /etc/os-release
```

O comando exibirá informações sobre a distribuição e a versão instalada.

Um resultado semelhante a este poderá ser apresentado:

```text
PRETTY_NAME="Debian GNU/Linux"
NAME="Debian GNU/Linux"
ID=debian
```

As informações exibidas dependem da versão do Debian instalada.

## Verificando o kernel

Também é possível verificar a versão do kernel utilizando:

```bash
uname -r
```

O comando apresentará a versão do kernel atualmente utilizada pelo sistema.

Exemplo:

```text
6.x.x-amd64
```

A versão exata dependerá da versão do Debian instalada.

## Verificando o armazenamento

Para verificar os discos e partições reconhecidos pelo sistema, utilize:

```bash
lsblk
```

Um resultado simplificado poderá apresentar uma estrutura semelhante a:

```text
NAME   SIZE TYPE
sda     20G disk
├─sda1  ... part
└─sda2  ... part
```

Os nomes das partições e seus tamanhos podem variar de acordo com o particionamento escolhido durante a instalação.

## Verificando a memória

A quantidade de memória reconhecida pelo Debian pode ser consultada utilizando:

```bash
free -h
```

O resultado deverá indicar aproximadamente a quantidade de memória disponibilizada para a máquina virtual.

Como a máquina foi configurada com:

```text
Memória RAM: 2048 MB
```

o sistema deverá reconhecer aproximadamente 2 GB de memória, considerando as diferenças decorrentes do próprio funcionamento do sistema.

## Verificando os processadores

Para verificar os processadores disponíveis para o sistema convidado, utilize:

```bash
nproc
```

Como a máquina virtual foi configurada com:

```text
Processadores: 2
```

o resultado esperado será semelhante a:

```text
2
```

## Verificando o nome da máquina

O nome configurado durante a instalação pode ser consultado utilizando:

```bash
hostname
```

O resultado esperado será semelhante a:

```text
debian-lab
```

## Resultado

Após concluir a instalação e realizar o primeiro acesso, teremos o Debian instalado dentro da máquina virtual.

A estrutura do laboratório será:

```text
Computador físico
       |
       +-- Windows
              |
              +-- Oracle VirtualBox
                     |
                     +-- debian-lab
                            |
                            +-- Debian
                            +-- 2 GB RAM
                            +-- 2 CPUs
                            +-- 20 GB Disco
                            +-- NAT
```

O sistema operacional agora está instalado no disco virtual e pode ser inicializado normalmente pelo Oracle VirtualBox.

## Configuração utilizada

| Recurso             | Configuração |
| ------------------- | ------------ |
| Máquina virtual     | `debian-lab` |
| Sistema operacional | Debian       |
| Memória RAM         | 2048 MB      |
| Processadores       | 2            |
| Disco virtual       | 20 GB        |
| Instalação          | Imagem ISO   |
| Rede inicial        | NAT          |

## Considerações finais

A instalação do Debian foi concluída dentro da máquina virtual criada no Oracle VirtualBox.

Neste momento, temos um sistema operacional funcional e preparado para receber as configurações adicionais necessárias para o laboratório.

A instalação utilizou uma configuração simples, com 2 GB de memória RAM, 2 processadores e um disco virtual de 20 GB.

A partir deste ponto, a máquina poderá ser utilizada para estudar Linux e posteriormente receber ferramentas e serviços relacionados a infraestrutura, redes, Docker, DevOps e outras tecnologias.

A configuração de rede ainda será abordada separadamente. Isso permitirá verificar como o Debian identifica sua interface de rede, obter um endereço IP e realizar testes de conectividade.

## Próxima etapa

Com o Debian instalado e funcionando, o próximo procedimento será configurar e testar a rede da máquina virtual.

O procedimento será documentado em:

```text
docs/windows/05-configurando-a-rede.md
```

