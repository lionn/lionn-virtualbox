# Criando uma Máquina Virtual no Oracle VirtualBox

## Introdução

Após instalar o Oracle VirtualBox no Windows, o próximo passo é criar a máquina virtual que será utilizada como ambiente de laboratório.

Neste documento será criada uma máquina virtual para instalação do Debian. Serão definidos os principais recursos de hardware virtual, incluindo memória RAM, processadores e armazenamento.

A configuração apresentada serve como base para um ambiente de estudos de Linux, infraestrutura, redes e DevOps.

## Objetivo

Ao final deste procedimento teremos uma máquina virtual criada no Oracle VirtualBox, preparada para receber a instalação do Debian.

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
Máquina Virtual
       |
       v
     Debian
```

## Pré-requisitos

Antes de iniciar, é necessário ter:

* Oracle VirtualBox instalado no Windows
* Imagem ISO do Debian
* Espaço disponível em disco
* Memória RAM suficiente para executar a máquina virtual
* Processador com suporte à virtualização

A instalação do VirtualBox é apresentada no documento:

```text
docs/windows/01-instalando-o-virtualbox.md
```

## Obtendo a imagem ISO do Debian

A máquina virtual precisará de uma imagem ISO para realizar a instalação do sistema operacional.

A imagem oficial do Debian pode ser obtida em:

https://www.debian.org/download

Após realizar o download, mantenha o arquivo ISO em um diretório de fácil localização.

Exemplo:

```text
C:\Users\usuario\Downloads\debian.iso
```

## Criando a máquina virtual

Abra o Oracle VirtualBox.

Na tela principal, selecione a opção **New** para iniciar o assistente de criação da máquina virtual.

```text
VirtualBox Manager
       |
       +-- New
```

## Definindo o nome da máquina

Informe um nome para identificar a máquina virtual.

Neste laboratório será utilizado:

```text
debian-lab
```

Ao informar o nome, o VirtualBox poderá identificar automaticamente o tipo de sistema operacional.

Para este laboratório, a máquina será configurada como:

```text
Nome: debian-lab
Tipo: Linux
Sistema: Debian
Arquitetura: 64-bit
```

## Selecionando a imagem ISO

Na etapa seguinte, selecione a imagem ISO do Debian obtida anteriormente.

Exemplo:

```text
C:\Users\usuario\Downloads\debian.iso
```

O VirtualBox utilizará essa imagem como mídia de instalação quando a máquina virtual for iniciada.

## Configurando a memória RAM

A memória RAM da máquina virtual será disponibilizada pelo computador físico.

Para este laboratório será utilizado:

```text
Memória RAM: 2048 MB
```

Essa configuração pode ser alterada posteriormente de acordo com os recursos disponíveis no computador.

É importante evitar a configuração de uma quantidade excessiva de memória, pois o sistema hospedeiro também precisa continuar dispondo de memória suficiente para funcionar.

## Configurando os processadores

O VirtualBox também permite definir quantos processadores virtuais serão disponibilizados para a máquina.

Para este laboratório será utilizado:

```text
Processadores: 2
```

Assim como a memória, essa configuração pode ser alterada posteriormente.

## Criando o disco virtual

A máquina virtual precisa de um dispositivo de armazenamento para instalar o sistema operacional.

Selecione a opção para criar um novo disco virtual.

```text
Armazenamento
       |
       +-- Criar novo disco virtual
```

## Definindo o tamanho do disco

Para este laboratório será utilizado um disco virtual com:

```text
Tamanho: 20 GB
```

O tamanho necessário depende da finalidade da máquina virtual.

Um ambiente destinado apenas a estudos básicos pode utilizar uma configuração menor. Já laboratórios que envolvem Docker, servidores, bancos de dados ou Magento 2 podem exigir uma quantidade significativamente maior de armazenamento.

## Revisando a configuração

Antes de criar a máquina virtual, revise as configurações definidas.

A configuração utilizada neste laboratório será:

```text
Nome: debian-lab
Sistema operacional: Debian
Memória RAM: 2048 MB
Processadores: 2
Disco virtual: 20 GB
```

## Criando a máquina virtual

Depois de revisar as configurações, confirme a criação da máquina virtual.

O VirtualBox criará os arquivos necessários para representar o hardware virtual e armazenará o disco virtual no diretório configurado.

Após a conclusão, a máquina deverá aparecer na lista de máquinas virtuais do VirtualBox Manager.

## Verificando a máquina virtual

Selecione a máquina virtual `debian-lab` no VirtualBox Manager e verifique as configurações.

A máquina deverá apresentar os recursos definidos anteriormente.

```text
debian-lab

Sistema:
    Linux / Debian

Memória:
    2048 MB

Processadores:
    2

Armazenamento:
    20 GB
```

## Resultado

Ao final deste procedimento, teremos uma máquina virtual criada e preparada para receber a instalação do Debian.

A estrutura do laboratório será:

```text
Windows
   |
   +-- Oracle VirtualBox
          |
          +-- debian-lab
                 |
                 +-- 2 GB RAM
                 +-- 2 CPUs
                 +-- 20 GB Disco
                 +-- ISO do Debian
```

Neste ponto, a máquina virtual ainda não possui o Debian instalado no disco virtual.

A instalação do sistema operacional será realizada na próxima etapa da documentação.

## Configuração utilizada

| Recurso             | Configuração |
| ------------------- | ------------ |
| Nome                | `debian-lab` |
| Sistema operacional | Debian       |
| Tipo                | Linux        |
| Arquitetura         | 64-bit       |
| Memória RAM         | 2048 MB      |
| Processadores       | 2            |
| Disco virtual       | 20 GB        |
| Rede                | NAT          |

## Considerações finais

A máquina virtual foi criada e seus principais recursos foram definidos.

Essa configuração fornece uma base simples para iniciar um laboratório Debian utilizando o Oracle VirtualBox.

A partir dela, será possível instalar o sistema operacional e posteriormente utilizar o ambiente para estudos de Linux, redes, servidores, Docker e outras tecnologias relacionadas à infraestrutura.

## Próxima etapa

A próxima etapa consiste em configurar os recursos da máquina virtual antes da instalação do sistema operacional.

O procedimento será documentado em:

```text
docs/windows/03-configurando-a-maquina-virtual.md
```
