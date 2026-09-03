# Virtualização

Virtualização é uma tecnologia que permite criar ambientes computacionais virtuais utilizando os recursos de um computador físico.

Em vez de cada sistema operacional precisar de um computador próprio, podemos utilizar um único equipamento físico para executar diferentes máquinas virtuais.

Cada máquina virtual possui recursos virtuais de processamento, memória, armazenamento e rede, permitindo executar um sistema operacional de forma independente dentro do ambiente virtualizado.

## Conceito de virtualização

Em um ambiente tradicional, podemos ter um computador físico executando diretamente um sistema operacional:

```text
Hardware físico
       |
       v
Windows
       |
       +-- Aplicações
```

Com a virtualização, uma camada de software permite criar máquinas virtuais sobre o sistema operacional existente:

```text
Hardware físico
       |
       v
Windows
       |
       v
Oracle VirtualBox
       |
       +------------------+
       |                  |
       v                  v
   Máquina 1          Máquina 2
    Debian              Linux
```

Dessa forma, diferentes sistemas operacionais podem ser executados no mesmo computador físico.

O Oracle VirtualBox é uma plataforma de virtualização que permite criar e executar essas máquinas virtuais.

## O que é uma máquina virtual?

Uma máquina virtual, ou VM (Virtual Machine), é um ambiente criado por um software de virtualização para executar um sistema operacional.

Para o sistema operacional guest, a máquina virtual apresenta recursos de hardware virtualizados.

Por exemplo:

```text
Máquina virtual
       |
       +-- CPU virtual
       +-- Memória RAM virtual
       +-- Disco virtual
       +-- Placa de rede virtual
       +-- Controladores virtuais
       +-- Dispositivos virtuais
```

O sistema operacional instalado dentro dessa máquina entende esses recursos como componentes de um computador.

No laboratório deste projeto teremos:

```text
Máquina virtual:
debian-lab

Sistema operacional:
Debian
```

## Host e Guest

Dois termos aparecem constantemente quando trabalhamos com virtualização: `host` e `guest`.

### Host

O host é o computador físico onde o software de virtualização está instalado.

Neste laboratório:

```text
Host:
Windows
```

O host fornece os recursos físicos utilizados pelas máquinas virtuais.

Entre esses recursos estão:

* Processador
* Memória RAM
* Armazenamento
* Rede
* Dispositivos físicos

### Guest

O guest é o sistema operacional executado dentro da máquina virtual.

Neste laboratório:

```text
Guest:
Debian
```

A relação pode ser representada assim:

```text
Computador físico
       |
       +-- Host: Windows
               |
               +-- Oracle VirtualBox
                       |
                       +-- Guest: Debian
```

A documentação oficial do VirtualBox utiliza justamente os conceitos de host para o sistema operacional do computador físico e guest para o sistema operacional executado dentro da VM.

## Hypervisor

O hypervisor é o componente responsável por fornecer e administrar o ambiente de virtualização.

Ele controla a utilização dos recursos físicos e apresenta recursos virtuais para as máquinas virtuais.

Existem dois modelos principais de hypervisor:

```text
Tipo 1
Bare Metal
```

e:

```text
Tipo 2
Hosted
```

## Hypervisor Tipo 1

Um hypervisor de tipo 1 é executado diretamente sobre o hardware físico.

A estrutura é:

```text
Hardware físico
       |
       v
Hypervisor
       |
       +-- Máquina virtual
       |
       +-- Máquina virtual
       |
       +-- Máquina virtual
```

Nesse modelo, não existe um sistema operacional convencional entre o hardware e o hypervisor.

Exemplos de tecnologias que utilizam esse modelo incluem plataformas voltadas para virtualização de servidores e data centers.

## Hypervisor Tipo 2

Um hypervisor de tipo 2 é executado sobre um sistema operacional existente.

A estrutura é:

```text
Hardware físico
       |
       v
Sistema operacional
       |
       v
Hypervisor
       |
       +-- Máquina virtual
       |
       +-- Máquina virtual
```

O Oracle VirtualBox é classificado pela própria Oracle como um hypervisor hospedado, também conhecido como hypervisor de tipo 2.

No nosso laboratório:

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

Isso permite utilizar o computador normalmente no Windows enquanto a máquina virtual Debian está em execução.

## Recursos físicos e recursos virtuais

Uma máquina virtual utiliza recursos físicos do computador host.

Por exemplo, suponha que o computador possua:

```text
CPU:
8 núcleos

RAM:
16 GB

Disco:
500 GB
```

Podemos criar uma máquina virtual utilizando uma parte desses recursos:

```text
debian-lab

CPU:
2 vCPUs

RAM:
2 GB

Disco:
20 GB
```

Durante a execução da VM, esses recursos são disponibilizados para o sistema operacional guest.

## CPU virtual

A CPU virtual, normalmente representada como `vCPU`, é o processador virtual disponibilizado para a máquina virtual.

Por exemplo:

```text
Computador físico
8 núcleos
     |
     +-- 2 vCPUs --> debian-lab
```

A quantidade de CPUs virtuais deve ser escolhida considerando os recursos disponíveis no host.

A configuração exagerada pode prejudicar tanto a máquina virtual quanto o sistema operacional principal.

Neste laboratório utilizaremos:

```text
2 vCPUs
```

## Memória virtual

A memória RAM também é compartilhada entre o host e as máquinas virtuais.

Por exemplo:

```text
Host:
16 GB RAM

        |
        +-- 2 GB --> debian-lab
        |
        +-- restante --> Windows e aplicações
```

A memória atribuída à VM deixa de estar disponível para o host enquanto a máquina virtual estiver utilizando esse recurso.

Por isso, a quantidade de memória deve ser planejada de acordo com os recursos físicos disponíveis.

Neste laboratório:

```text
RAM:
2048 MB
```

A documentação do VirtualBox também alerta que a memória atribuída à VM não fica disponível para o sistema operacional host enquanto a máquina virtual estiver em execução.

## Disco virtual

Uma máquina virtual normalmente utiliza um arquivo ou conjunto de arquivos no armazenamento do host para representar seu disco virtual.

Podemos imaginar:

```text
Windows
   |
   +-- Disco físico
         |
         +-- Arquivos da VM
               |
               +-- debian-lab.vdi
```

Dentro do Debian, esse recurso aparece como um disco.

Por exemplo:

```text
Debian
   |
   +-- /dev/sda
```

O sistema operacional guest não precisa conhecer os detalhes de como o arquivo do disco virtual é armazenado pelo host.

Para ele, o dispositivo funciona como um disco.

## Disco físico x disco virtual

A diferença pode ser representada assim:

```text
Disco físico
      |
      v
Hardware real
      |
      v
Sistema operacional host
```

Enquanto:

```text
Disco virtual
      |
      v
Arquivo armazenado no host
      |
      v
Oracle VirtualBox
      |
      v
Sistema operacional guest
```

Essa abstração permite criar, mover, copiar e administrar máquinas virtuais sem precisar instalar um disco físico exclusivo para cada sistema operacional.

## Rede virtual

A virtualização também permite criar interfaces de rede virtuais.

A máquina virtual possui uma placa de rede virtual que é administrada pelo VirtualBox.

Podemos representar:

```text
Debian
   |
   v
Placa de rede virtual
   |
   v
Oracle VirtualBox
   |
   v
Placa de rede física
   |
   v
Rede
```

O VirtualBox possui diferentes modos de rede.

Entre eles estão:

* NAT
* Bridged Adapter
* Host-only Adapter
* Internal Network

Cada modo possui uma finalidade diferente.

Neste laboratório será utilizado inicialmente o modo:

```text
NAT
```

A configuração prática da rede será apresentada posteriormente na documentação do Windows.

## NAT

O modo NAT permite que a máquina virtual utilize a conexão de rede do host para acessar redes externas.

Uma representação simplificada:

```text
Debian
   |
   v
Rede virtual
   |
   v
VirtualBox NAT
   |
   v
Windows
   |
   v
Internet
```

Esse modo é bastante conveniente para uma máquina virtual de laboratório porque normalmente permite acesso à Internet sem exigir uma configuração mais complexa na rede física.

## Bridged Adapter

No modo Bridged Adapter, a máquina virtual é conectada à rede física através da interface de rede do host.

A estrutura pode ser representada assim:

```text
Debian
   |
   v
Placa virtual
   |
   v
VirtualBox
   |
   v
Interface física do Windows
   |
   v
Rede local
```

Nesse cenário, a máquina virtual pode participar da rede como outro dispositivo.

Esse modo é útil em determinados laboratórios onde é necessário que a VM seja acessível diretamente por outros dispositivos da rede.

## Host-only Adapter

O modo Host-only permite criar uma rede entre o host e as máquinas virtuais sem necessariamente fornecer acesso direto à rede externa.

Por exemplo:

```text
Windows
   |
   +----------------+
                    |
                    v
              Rede Host-only
                    |
                    +-- Debian
                    |
                    +-- outra VM
```

Esse tipo de configuração pode ser útil para criar laboratórios isolados.

## Internal Network

O modo Internal Network permite criar uma rede utilizada apenas pelas máquinas virtuais conectadas a ela.

Por exemplo:

```text
             Internal Network
                    |
          +---------+---------+
          |                   |
          v                   v
       Debian 1            Debian 2
```

Esse cenário pode ser interessante para simular redes internas e ambientes com múltiplos servidores.

## Virtualização de hardware

Para executar máquinas virtuais de forma eficiente, o processador físico precisa oferecer recursos de virtualização por hardware.

Em processadores Intel, essa tecnologia está associada ao:

```text
Intel VT-x
```

Em processadores AMD:

```text
AMD-V
```

Esses recursos permitem que o software de virtualização utilize mecanismos específicos do processador para executar máquinas virtuais.

O VirtualBox utiliza extensões de virtualização por hardware quando disponíveis e configuradas no sistema.

## Virtualização e desempenho

A máquina virtual não possui recursos físicos próprios.

Ela utiliza os recursos disponíveis no computador host.

Por isso, o desempenho da VM depende de fatores como:

* Processador
* Memória RAM
* Velocidade do armazenamento
* Configuração da máquina virtual
* Sistema operacional guest
* Carga de trabalho
* Quantidade de máquinas virtuais em execução

Por exemplo:

```text
Host com poucos recursos
        |
        v
VM com muitos recursos
        |
        v
Possível degradação de desempenho
```

O planejamento dos recursos é importante para manter tanto o host quanto o guest funcionando adequadamente.

## Isolamento

Uma das características importantes da virtualização é o isolamento entre o guest e o host.

A máquina virtual executa o sistema operacional dentro de um ambiente controlado pelo software de virtualização.

De maneira simplificada:

```text
Windows
   |
   v
Oracle VirtualBox
   |
   +-- Ambiente virtual
           |
           +-- Debian
```

Isso permite realizar testes no guest sem instalar diretamente os componentes testados no sistema operacional principal.

Entretanto, virtualização não deve ser interpretada como uma barreira de segurança absoluta.

Máquinas virtuais ainda devem ser administradas e protegidas adequadamente.

## Virtualização para desenvolvimento e testes

Um dos usos mais comuns de máquinas virtuais é criar ambientes de desenvolvimento e testes.

Por exemplo:

```text
Computador pessoal
       |
       v
Oracle VirtualBox
       |
       +-- Debian
             |
             +-- Nginx
             +-- PHP
             +-- MariaDB
             +-- Redis
             +-- Docker
             +-- aplicações
```

Esse ambiente permite realizar testes sem transformar o computador principal em um servidor de laboratório.

A própria documentação do VirtualBox destaca seu uso para desenvolvimento e testes, incluindo investigação de problemas relacionados a configurações de software e rede.

## Virtualização para estudos

Para estudos de infraestrutura e DevOps, a virtualização permite reproduzir diversos cenários.

Por exemplo:

```text
Laboratório
    |
    +-- Debian
    |
    +-- Docker
    |
    +-- Nginx
    |
    +-- Banco de dados
    |
    +-- Git
    |
    +-- CI/CD
```

Também podemos criar várias máquinas virtuais:

```text
VirtualBox
    |
    +-- Debian Web
    |
    +-- Debian Database
    |
    +-- Debian Docker
    |
    +-- Debian Test
```

Isso possibilita simular uma pequena infraestrutura utilizando apenas um computador físico.

## Virtualização não é emulação

Virtualização e emulação são conceitos diferentes.

Na virtualização, o sistema guest pode utilizar diretamente ou de forma assistida recursos da arquitetura de hardware compatível com o host.

Na emulação, o software pode simular uma arquitetura diferente daquela existente fisicamente.

Uma comparação simplificada:

```text
Virtualização

CPU x86_64
    |
    v
VM x86_64
```

Enquanto:

```text
Emulação

CPU x86_64
    |
    v
Software de emulação
    |
    v
Arquitetura diferente
```

A virtualização tende a oferecer melhor desempenho quando o hardware e o sistema guest são compatíveis com a arquitetura utilizada.

## Virtualização e portabilidade

Máquinas virtuais também podem facilitar a movimentação de ambientes entre computadores.

O VirtualBox utiliza formatos de arquivos de máquinas virtuais que permitem transportar VMs entre diferentes hosts compatíveis.

Por exemplo:

```text
Windows
   |
   v
Máquina virtual Debian
   |
   v
Exportação
   |
   v
Outro computador
   |
   v
Importação
   |
   v
Máquina virtual Debian
```

A documentação do VirtualBox também destaca a possibilidade de importar e exportar máquinas virtuais utilizando formatos como OVF.

## Virtualização e snapshots

Snapshots são outro recurso importante para laboratórios.

Podemos criar um ponto de recuperação antes de realizar uma alteração.

Por exemplo:

```text
Debian funcionando
       |
       v
Snapshot
       |
       v
Instalar software
       |
       v
Alterar configuração
       |
       v
Realizar testes
```

Se algo der errado, podemos retornar ao estado registrado pelo snapshot.

Esse recurso será apresentado posteriormente na documentação específica do Windows.

## Virtualização no nosso laboratório

Neste projeto será utilizado o seguinte ambiente:

```text
Hardware físico
       |
       v
Windows
       |
       v
Oracle VirtualBox
       |
       v
debian-lab
       |
       v
Debian
```

A máquina virtual terá inicialmente:

```text
Nome:
debian-lab

CPU:
2 vCPUs

RAM:
2048 MB

Disco:
20 GB

Rede:
NAT
```

Essa configuração será utilizada como base para os procedimentos práticos.

## Fluxo do laboratório

Depois de entender os conceitos de virtualização, o laboratório será construído progressivamente.

A sequência será:

```text
Introdução
    |
    v
Virtualização
    |
    v
Instalação do VirtualBox
    |
    v
Criação da VM
    |
    v
Configuração da VM
    |
    v
Instalação do Debian
    |
    v
Configuração da rede
    |
    v
Pastas compartilhadas
    |
    v
Snapshots
```

A parte conceitual termina aqui.

A partir do próximo documento começa a configuração prática do ambiente no Windows.

## Resumo

Virtualização permite criar computadores virtuais dentro de um computador físico.

Os principais conceitos apresentados neste documento foram:

| Conceito      | Descrição                                             |
| ------------- | ----------------------------------------------------- |
| Host          | Sistema operacional do computador físico              |
| Guest         | Sistema operacional executado dentro da VM            |
| VM            | Ambiente virtual onde o guest é executado             |
| Hypervisor    | Software responsável pela virtualização               |
| vCPU          | Processador virtual atribuído à VM                    |
| RAM virtual   | Memória disponibilizada para a VM                     |
| Disco virtual | Armazenamento utilizado pela VM                       |
| Rede virtual  | Interface de rede apresentada à VM                    |
| NAT           | Modo de rede utilizado inicialmente neste laboratório |
| Snapshot      | Ponto de recuperação da VM                            |

## Considerações

A virtualização é uma ferramenta importante para desenvolvimento, testes, estudos de infraestrutura e administração de sistemas.

Neste projeto, o Oracle VirtualBox será utilizado para transformar um computador Windows em um ambiente de laboratório capaz de executar o Debian e, posteriormente, outras tecnologias.

Com os conceitos apresentados, já podemos partir para a instalação do software de virtualização.

## Próximos passos

O próximo documento inicia a parte prática do projeto.

Será realizada a instalação do Oracle VirtualBox no Windows.

Próximo documento:

```text
docs/windows/01-instalando-o-virtualbox.md
```

A partir desse ponto, os documentos da pasta `windows/` apresentarão passo a passo a construção do laboratório `debian-lab`.
