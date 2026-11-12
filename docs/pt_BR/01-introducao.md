# Introdução ao Oracle VirtualBox

O Oracle VirtualBox é uma plataforma de virtualização que permite executar diferentes sistemas operacionais dentro de máquinas virtuais.

Em vez de instalar um sistema operacional diretamente no computador físico, podemos criar uma máquina virtual que possui recursos virtuais de processamento, memória, armazenamento e rede.

Isso permite criar ambientes isolados para estudos, desenvolvimento, testes e laboratórios de infraestrutura.

Neste projeto será utilizado o Oracle VirtualBox para criar um laboratório baseado em Debian, utilizando inicialmente um computador com Windows como sistema operacional hospedeiro.

## Objetivo do projeto

O objetivo deste projeto é documentar, de forma prática e progressiva, a criação e utilização de uma máquina virtual para estudos de Linux, infraestrutura, redes, Docker e DevOps.

Durante o laboratório serão abordados conceitos e procedimentos como:

* Instalação do Oracle VirtualBox
* Criação de uma máquina virtual
* Configuração de memória e CPU
* Configuração de armazenamento
* Configuração de rede
* Instalação do Debian
* Instalação das Guest Additions
* Configuração de pastas compartilhadas
* Criação e utilização de snapshots
* Administração básica da máquina virtual

A ideia é começar com uma máquina virtual simples e, posteriormente, utilizar esse ambiente como base para outros laboratórios.

## O que é virtualização?

Virtualização é uma tecnologia que permite utilizar recursos físicos de um computador para criar ambientes computacionais virtuais.

Um único computador físico pode executar várias máquinas virtuais simultaneamente.

Por exemplo:

```text
Computador físico
       |
       v
+----------------------+
|   Sistema Windows    |
|                      |
|  Oracle VirtualBox   |
+----------------------+
       |
       +----------------------+
       |                      |
       v                      v
+-------------+        +-------------+
| debian-lab  |        | outra VM    |
| Debian      |        | Linux       |
+-------------+        +-------------+
```

Cada máquina virtual possui seus próprios recursos virtuais e pode executar um sistema operacional independente.

## Máquina física e máquina virtual

Para entender o funcionamento do VirtualBox, é importante diferenciar alguns conceitos.

### Host

O host é o computador físico onde o Oracle VirtualBox está instalado.

Neste laboratório:

```text
Host:
Windows
```

O host fornece os recursos físicos utilizados pelas máquinas virtuais, como:

* Processador
* Memória RAM
* Armazenamento
* Interface de rede
* Dispositivos USB
* Outros recursos de hardware

### Guest

Guest é o sistema operacional executado dentro da máquina virtual.

Neste laboratório:

```text
Guest:
Debian
```

O Debian não está sendo instalado diretamente no hardware físico.

Ele será executado dentro da máquina virtual criada pelo VirtualBox.

### Máquina Virtual

A máquina virtual é o ambiente criado pelo VirtualBox para executar o sistema operacional guest.

Neste projeto:

```text
Máquina virtual:
debian-lab
```

A VM possui recursos virtuais, como:

```text
CPU virtual
RAM virtual
Disco virtual
Placa de rede virtual
Controladores virtuais
```

Esses recursos são apresentados ao sistema operacional guest como se fossem componentes de um computador.

## Estrutura do laboratório

O laboratório deste projeto será organizado da seguinte maneira:

```text
Windows
   |
   v
Oracle VirtualBox
   |
   v
Máquina Virtual
debian-lab
   |
   v
Debian
   |
   +-- Rede
   |
   +-- Guest Additions
   |
   +-- Pasta compartilhada
   |
   +-- Snapshots
```

Essa estrutura será utilizada como base para os próximos estudos.

## Por que utilizar uma máquina virtual?

Máquinas virtuais são muito úteis para ambientes de estudo porque permitem experimentar diferentes configurações sem modificar diretamente o sistema operacional principal.

Por exemplo, podemos utilizar uma VM para:

* Instalar um servidor Linux
* Testar configurações de rede
* Instalar serviços
* Estudar comandos Linux
* Testar Docker
* Configurar Nginx
* Configurar PHP
* Configurar bancos de dados
* Testar aplicações
* Simular ambientes de infraestrutura
* Estudar ferramentas DevOps

Se uma configuração causar problemas, podemos utilizar recursos como snapshots para retornar a um estado anterior da máquina.

## VirtualBox como ambiente de laboratório

O Oracle VirtualBox é particularmente útil para estudos e testes porque permite criar máquinas virtuais em um computador que já possui um sistema operacional instalado.

Por exemplo:

```text
Windows
   |
   +-- VirtualBox
         |
         +-- Debian
         |
         +-- Ubuntu
         |
         +-- Windows Server
         |
         +-- outras VMs
```

A quantidade de máquinas virtuais que pode ser executada simultaneamente depende principalmente dos recursos disponíveis no computador físico.

Quanto mais memória RAM, CPU e armazenamento estiverem disponíveis, maior será a capacidade do host para executar máquinas virtuais.

## Hypervisor

O software responsável por criar e administrar o ambiente de virtualização é chamado de hypervisor.

O Oracle VirtualBox é classificado como um hypervisor hospedado, também conhecido como hypervisor de tipo 2.

Nesse modelo, existe um sistema operacional instalado no computador físico.

A estrutura pode ser representada assim:

```text
Hardware físico
       |
       v
Sistema operacional host
       |
       v
Oracle VirtualBox
       |
       v
Sistema operacional guest
```

Neste projeto:

```text
Hardware
   |
   v
Windows
   |
   v
Oracle VirtualBox
   |
   v
Debian
```

Isso é diferente de uma arquitetura em que o hypervisor é executado diretamente sobre o hardware físico.

## Recursos virtuais

Uma máquina virtual possui recursos que são apresentados ao sistema operacional guest como hardware virtual.

Entre eles estão:

### CPU

Podemos definir quantos processadores virtuais serão disponibilizados para a VM.

Neste laboratório:

```text
CPU:
2 vCPUs
```

### Memória RAM

A quantidade de memória disponível para a máquina virtual também pode ser configurada.

Neste laboratório:

```text
RAM:
2048 MB
```

### Armazenamento

A máquina virtual utilizará um disco virtual.

Neste laboratório:

```text
Disco:
20 GB
```

Esse disco será utilizado pelo Debian durante a instalação e posteriormente para os demais testes.

### Rede

O VirtualBox fornece interfaces de rede virtuais que permitem conectar a máquina virtual ao host, a outras máquinas virtuais ou à rede externa, dependendo do modo de rede configurado.

Inicialmente será utilizado:

```text
Modo:
NAT
```

A configuração detalhada será realizada posteriormente na documentação específica do Windows.

## Sistema operacional do laboratório

O sistema operacional utilizado neste projeto será o Debian.

O Debian é uma distribuição Linux amplamente utilizada em ambientes de servidores, infraestrutura e desenvolvimento.

Ele também é uma excelente opção para um laboratório de estudos porque permite trabalhar diretamente com conceitos importantes de administração Linux.

Neste projeto, a máquina virtual será chamada:

```text
debian-lab
```

## Configuração inicial do laboratório

A configuração planejada para a máquina virtual será:

| Recurso             | Configuração      |
| ------------------- | ----------------- |
| Nome                | `debian-lab`      |
| Sistema operacional | Debian            |
| CPU                 | 2 vCPUs           |
| Memória             | 2048 MB           |
| Disco               | 20 GB             |
| Rede                | NAT               |
| Host                | Windows           |
| Hypervisor          | Oracle VirtualBox |

Essa configuração é suficiente para o laboratório inicial.

Dependendo dos testes realizados posteriormente, os recursos da máquina virtual poderão ser ajustados.

## Guest Additions

O Oracle VirtualBox também possui um conjunto de ferramentas chamado Guest Additions.

Esses componentes são instalados dentro do sistema operacional guest e fornecem recursos adicionais de integração entre a máquina virtual e o host.

Entre os recursos disponíveis estão:

* Melhor integração do mouse
* Ajuste automático de resolução
* Integração com a área de transferência
* Pastas compartilhadas
* Recursos gráficos adicionais
* Melhor integração entre host e guest

Neste laboratório, as Guest Additions serão utilizadas principalmente para permitir a configuração de pastas compartilhadas entre Windows e Debian.

A instalação será realizada posteriormente.

## Pastas compartilhadas

Uma pasta compartilhada permite disponibilizar um diretório do computador host para a máquina virtual.

Por exemplo:

```text
Windows
C:\VirtualBox\Shared
        |
        v
Oracle VirtualBox
        |
        v
Debian
/mnt/shared
```

Isso facilita a transferência de arquivos entre o Windows e o Debian durante os estudos.

A configuração desse recurso será abordada em:

```text
docs/windows/06-pastas-compartilhadas.md
```

## Snapshots

Outro recurso importante do VirtualBox é o snapshot.

Um snapshot representa um estado específico da máquina virtual que pode ser restaurado posteriormente.

Por exemplo:

```text
Debian instalado
       |
       v
Configuração inicial
       |
       v
Snapshot
       |
       v
Novos testes
       |
       v
Alterações
```

Se um teste causar um problema, podemos utilizar o snapshot para retornar a um estado anterior da máquina virtual.

Snapshots são especialmente úteis em ambientes de laboratório e testes.

Eles não devem, entretanto, ser tratados como substitutos de uma estratégia de backup.

A utilização de snapshots será apresentada posteriormente no projeto.

## Laboratório e estudos de DevOps

A máquina virtual criada neste projeto poderá servir como base para outros laboratórios.

Depois que o Debian estiver instalado e configurado, podemos utilizar a VM para estudar tecnologias como:

```text
Linux
   |
   +-- Shell
   +-- SSH
   +-- Redes
   +-- Nginx
   +-- PHP
   +-- MariaDB
   +-- Redis
   +-- Docker
   +-- Git
   +-- Automação
   +-- CI/CD
   +-- DevOps
```

Isso permite utilizar uma única máquina física como ambiente de estudos para diferentes tecnologias.

## Virtualização e ambientes de teste

Uma das principais vantagens da virtualização é permitir a criação de ambientes isolados.

Por exemplo, podemos testar uma alteração no Debian sem precisar alterar diretamente o Windows.

```text
Windows
   |
   +-- Oracle VirtualBox
          |
          +-- Debian laboratório
                  |
                  +-- Testes
                  +-- Configurações
                  +-- Serviços
                  +-- Experimentos
```

Esse modelo é bastante útil durante o aprendizado porque permite experimentar configurações diferentes e reconstruir o ambiente quando necessário.

## O que será construído neste projeto

Ao longo da documentação será construída uma máquina virtual Debian funcional.

Antes de iniciar os procedimentos práticos, serão apresentados os conceitos fundamentais de virtualização.

O processo geral seguirá esta sequência:

```text
01
|
v
Introdução
|
v
02
|
v
Virtualização
|
v
Windows
|
+-- 01 Instalação do VirtualBox
|
+-- 02 Criação da máquina virtual
|
+-- 03 Configuração da máquina virtual
|
+-- 04 Instalação do Debian
|
+-- 05 Configuração da rede
|
+-- 06 Pastas compartilhadas
|
+-- 07 Snapshots
```

Ao final, teremos um laboratório funcional pronto para receber novos estudos.

## Estrutura da documentação

A documentação está organizada inicialmente em duas partes: conceitos gerais e procedimentos específicos para o sistema operacional utilizado como host.

Atualmente, o projeto possui a seguinte estrutura:

```text
docs/
├── 01-introducao.md
├── 02-virtualizacao.md
└── windows/
    ├── 01-instalando-o-virtualbox.md
    ├── 02-criando-a-maquina-virtual.md
    ├── 03-configurando-a-maquina-virtual.md
    ├── 04-instalando-o-debian.md
    ├── 05-configurando-a-rede.md
    ├── 06-pastas-compartilhadas.md
    └── 07-snapshots.md
```

A documentação para Linux será adicionada posteriormente, mantendo a mesma organização do projeto.

## Considerações

O objetivo deste laboratório não é apenas aprender a instalar o Oracle VirtualBox.

A proposta é construir uma base de infraestrutura que possa ser utilizada para estudos posteriores.

A partir de uma máquina virtual Debian, será possível experimentar diferentes tecnologias e conceitos sem depender de um servidor físico dedicado.

Esse tipo de ambiente também permite reproduzir cenários, testar configurações e documentar procedimentos de forma organizada.

## Próximos passos

Antes de iniciar a instalação do Oracle VirtualBox, o próximo documento apresenta os conceitos fundamentais relacionados à virtualização.

Próximo documento:

```text
docs/02-virtualizacao.md
```

Depois da introdução aos conceitos de virtualização, será iniciada a configuração prática do laboratório no Windows.

A documentação seguirá então para:

```text
docs/windows/01-instalando-o-virtualbox.md
```

