# lionn-virtualbox

Guia prático para instalação, configuração e utilização do Oracle VirtualBox em ambientes Windows e Linux.

Este projeto foi criado para documentar, de forma prática e progressiva, a criação e administração de máquinas virtuais utilizadas em laboratórios de estudo de Linux, infraestrutura, Docker e DevOps.

---

## Status

**Em desenvolvimento.**

A documentação está sendo construída de forma progressiva, começando pelos conceitos de virtualização e pelo laboratório utilizando Windows como sistema hospedeiro.

---

## Objetivos

* Entender os conceitos básicos de virtualização
* Conhecer o funcionamento de máquinas virtuais
* Instalar o Oracle VirtualBox
* Criar e configurar máquinas virtuais
* Configurar memória, CPU, armazenamento e rede
* Instalar sistemas operacionais Linux em máquinas virtuais
* Criar ambientes de laboratório para estudos
* Trabalhar com snapshots
* Configurar pastas compartilhadas entre host e guest
* Documentar procedimentos para ambientes Windows e Linux

---

## Conteúdo

### Conceitos

A documentação começa pelos fundamentos necessários para entender o funcionamento da virtualização.

* Introdução
* Virtualização
* Máquinas virtuais
* Host e Guest
* Hypervisor
* Recursos virtuais
* Redes virtuais
* Snapshots
* Virtualização para laboratórios

### Windows

A primeira parte prática do projeto utiliza o Windows como sistema hospedeiro.

* Instalação do Oracle VirtualBox
* Criação de uma máquina virtual
* Configuração da máquina virtual
* Instalação do Debian
* Configuração da rede
* Pastas compartilhadas
* Snapshots

### Linux

A documentação para Linux será adicionada progressivamente.

---

## Estrutura

```text
lionn-virtualbox/
├── assets/
├── docs/
│   ├── 01-introducao.md
│   ├── 02-virtualizacao.md
│   └── windows/
│       ├── 01-instalando-o-virtualbox.md
│       ├── 02-criando-a-maquina-virtual.md
│       ├── 03-configurando-a-maquina-virtual.md
│       ├── 04-instalando-o-debian.md
│       ├── 05-configurando-a-rede.md
│       ├── 06-pastas-compartilhadas.md
│       └── 07-snapshots.md
├── scripts/
├── .gitignore
└── README.md
```

---

## Documentação

### Introdução

Apresenta o objetivo do projeto, a organização da documentação e a proposta do laboratório.

`docs/01-introducao.md`

### Virtualização

Apresenta os principais conceitos relacionados à virtualização, máquinas virtuais, hypervisors, recursos virtuais e redes.

`docs/02-virtualizacao.md`

### Laboratório Windows

A documentação prática começa com a instalação e configuração do Oracle VirtualBox no Windows.

`docs/windows/01-instalando-o-virtualbox.md`

A partir desse ponto, o laboratório segue a seguinte sequência:

```text
Instalação do VirtualBox
        ↓
Criação da máquina virtual
        ↓
Configuração da máquina virtual
        ↓
Instalação do Debian
        ↓
Configuração da rede
        ↓
Pastas compartilhadas
        ↓
Snapshots
```

---

## Laboratório

O laboratório utilizado na documentação possui como objetivo criar uma máquina virtual Debian para estudos.

Configuração inicial:

```text
Máquina virtual: debian-lab
Sistema operacional: Debian
CPU: 2 vCPUs
Memória RAM: 2048 MB
Disco virtual: 20 GB
Rede: NAT
```

Essa máquina virtual servirá como base para outros estudos relacionados a Linux, infraestrutura e DevOps.

---

## Próximas etapas

Após a conclusão da documentação inicial para Windows, o projeto será expandido para incluir:

* Laboratório utilizando Linux como host
* Configuração avançada de redes virtuais
* Administração de máquinas virtuais
* Automação utilizando VBoxManage
* Integração com outros laboratórios
* Scripts para criação e configuração de máquinas virtuais

---

## Integração com outros estudos

O laboratório criado neste projeto pode ser utilizado como base para estudar outras tecnologias, como:

* Linux
* Docker
* Nginx
* PHP
* MariaDB
* Redis
* OpenSearch
* Magento 2
* DevOps
* Automação

A ideia é que o VirtualBox funcione como uma das bases para a construção de ambientes de laboratório utilizados nos demais projetos.

---

## Projeto

Este repositório faz parte dos estudos e laboratórios publicados em:

**lionn.net**

---

## Licença

Este projeto está disponível para fins educacionais.

