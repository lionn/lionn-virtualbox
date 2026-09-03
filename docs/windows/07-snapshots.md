# Snapshots no Oracle VirtualBox

Snapshots permitem salvar o estado de uma máquina virtual em determinado momento para que ele possa ser restaurado posteriormente.

Esse recurso é especialmente útil em ambientes de laboratório, onde é comum instalar softwares, alterar configurações e realizar testes que podem modificar o sistema.

Neste documento será utilizado o laboratório criado nas etapas anteriores:

```text
Máquina virtual: debian-lab
Sistema operacional: Debian
Memória RAM: 2048 MB
CPU: 2
Disco: 20 GB
Rede: NAT
```

## Objetivo

Ao final deste documento, será possível:

* Entender o conceito de snapshot
* Criar um snapshot
* Adicionar nome e descrição
* Visualizar snapshots existentes
* Restaurar um snapshot
* Excluir um snapshot
* Utilizar snapshots durante testes
* Entender as diferenças entre snapshot e backup
* Utilizar o `VBoxManage` para administrar snapshots

## O que é um Snapshot?

Um snapshot representa um ponto específico no estado de uma máquina virtual.

Podemos imaginar um snapshot como uma fotografia da VM naquele momento.

Por exemplo:

```text
Debian instalado
       |
       v
Configuração inicial
       |
       v
Snapshot: Debian inicial
       |
       v
Instalar novos softwares
       |
       v
Alterar configurações
       |
       v
Realizar testes
```

Se alguma alteração causar um problema, o snapshot pode ser utilizado para retornar a máquina virtual ao estado em que ela estava quando o snapshot foi criado.

```text
Snapshot
   |
   v
Debian inicial
   |
   +---- alterações
   |
   +---- instalações
   |
   +---- testes
   |
   +---- problema
   |
   v
Restaurar
   |
   v
Debian inicial
```

O VirtualBox mantém as informações necessárias para retornar a VM ao estado registrado pelo snapshot.

## Snapshot não é Backup

É importante não confundir snapshot com backup.

Um snapshot é um recurso de gerenciamento da máquina virtual e deve ser utilizado principalmente para facilitar testes, alterações e recuperação rápida de um estado anterior.

Um backup possui outro objetivo: manter uma cópia dos dados para recuperação em caso de perda, corrupção, falha de hardware ou outro incidente.

Uma comparação simples:

| Recurso                  | Snapshot                           | Backup                |
| ------------------------ | ---------------------------------- | --------------------- |
| Objetivo principal       | Retornar a VM a um estado anterior | Recuperar dados       |
| Uso comum                | Laboratórios e testes              | Proteção de dados     |
| Mantém histórico da VM   | Sim                                | Depende da estratégia |
| Substitui backup         | Não                                | Não se aplica         |
| Pode consumir espaço     | Sim                                | Sim                   |
| Útil antes de alterações | Sim                                | Sim                   |

Portanto, snapshots não devem ser utilizados como única estratégia de proteção dos dados.

## Como os Snapshots Funcionam

Ao criar um snapshot, o VirtualBox preserva o estado da máquina virtual naquele momento.

Além das configurações da VM, o estado dos discos virtuais também é considerado.

Depois que o snapshot é criado, novas alterações realizadas no disco passam a ser registradas de forma diferenciada.

De maneira simplificada:

```text
Estado inicial
     |
     v
Snapshot
     |
     +----------------+
     |                |
     v                v
Estado preservado    Novas alterações
                     |
                     +-- arquivos
                     +-- instalações
                     +-- configurações
```

Por isso, quanto mais tempo a VM continuar sendo utilizada depois da criação de um snapshot, maior pode ser o espaço utilizado pelas alterações associadas a ele.

O VirtualBox utiliza imagens diferenciais para armazenar essas alterações.

## Quando Utilizar Snapshots

Snapshots são bastante úteis antes de alterações que podem modificar significativamente o ambiente.

Alguns exemplos:

* Instalação de novos softwares
* Alterações em configurações do sistema
* Testes de servidores
* Testes de rede
* Instalação de Docker
* Instalação de bancos de dados
* Testes com Nginx
* Testes com PHP
* Alterações no sistema de arquivos
* Laboratórios de infraestrutura
* Estudos de Linux

Por exemplo, antes de instalar o Docker:

```text
Debian funcionando
       |
       v
Snapshot: antes-do-docker
       |
       v
Instalação do Docker
       |
       v
Testes
```

Caso alguma coisa dê errado, o snapshot pode ser restaurado.

## Criando um Snapshot

Antes de criar o snapshot, é interessante deixar a máquina virtual em um estado conhecido.

Neste laboratório, será utilizado o estado atual da máquina `debian-lab`.

Abra o Oracle VirtualBox Manager.

Selecione:

```text
debian-lab
```

Acesse a área:

```text
Snapshots
```

Na interface de gerenciamento de snapshots, selecione o estado atual da máquina e escolha a opção:

```text
Take
```

Dependendo da versão e do idioma da interface, o botão pode aparecer como:

```text
Tirar
```

Será exibida uma janela solicitando informações sobre o snapshot.

Utilize:

```text
Nome:
Debian inicial

Descrição:
Estado inicial do laboratório após instalação do Debian,
configuração de rede e configuração de pastas compartilhadas.
```

A descrição é útil para registrar exatamente o motivo pelo qual aquele snapshot foi criado.

Depois de confirmar, o snapshot será exibido na árvore de snapshots.

A estrutura ficará semelhante a:

```text
debian-lab
└── Debian inicial
    └── Current State
```

O item `Current State` representa o estado atual da máquina virtual a partir daquele snapshot.

## Criando um Snapshot com a Máquina em Execução

Também é possível criar um snapshot enquanto a máquina virtual está em execução.

Nesse caso, o VirtualBox pausa a VM durante a criação do snapshot e depois continua sua execução.

Para este laboratório, entretanto, é recomendável realizar alterações importantes com a máquina em um estado controlado e, quando possível, criar snapshots com a VM desligada.

Isso facilita a identificação do estado que está sendo preservado.

## Verificando o Snapshot

Depois de criar o snapshot, selecione:

```text
Debian inicial
```

A interface do VirtualBox permite visualizar informações relacionadas ao snapshot.

Também é possível utilizar o terminal do Windows através do `VBoxManage`.

Abra o PowerShell ou o Prompt de Comando e execute:

```powershell
VBoxManage snapshot "debian-lab" list
```

O comando deverá apresentar o snapshot existente.

Para obter informações mais detalhadas:

```powershell
VBoxManage snapshot "debian-lab" list --details
```

## Criando Snapshot pelo VBoxManage

Além da interface gráfica, o VirtualBox fornece o utilitário `VBoxManage`.

Para criar um snapshot:

```powershell
VBoxManage snapshot "debian-lab" take "antes-dos-testes"
```

Também é possível adicionar uma descrição:

```powershell
VBoxManage snapshot "debian-lab" take "antes-dos-testes" --description="Estado da VM antes dos testes de laboratório"
```

O `VBoxManage` permite automatizar tarefas de administração do VirtualBox através da linha de comando.

## Listando Snapshots

Para listar os snapshots da máquina virtual:

```powershell
VBoxManage snapshot "debian-lab" list
```

Para visualizar informações detalhadas:

```powershell
VBoxManage snapshot "debian-lab" list --details
```

Essa abordagem é útil principalmente quando o VirtualBox começa a fazer parte de processos automatizados ou scripts de laboratório.

## Restaurando um Snapshot

A restauração faz a máquina virtual retornar ao estado representado pelo snapshot selecionado.

Por exemplo:

```text
Debian inicial
       |
       v
Instalar software
       |
       v
Alterar configurações
       |
       v
Problema
       |
       v
Restaurar "Debian inicial"
```

Para restaurar pela interface gráfica:

1. Desligue a máquina virtual ou deixe-a em um estado compatível com a operação.
2. Abra o Oracle VirtualBox Manager.
3. Selecione `debian-lab`.
4. Acesse `Snapshots`.
5. Selecione `Debian inicial`.
6. Clique em `Restore`.

O VirtualBox retornará a máquina virtual ao estado representado pelo snapshot.

## Atenção ao Restaurar

A restauração de um snapshot pode causar perda das alterações realizadas depois que o snapshot foi criado.

Por exemplo, suponha que o snapshot tenha sido criado quando existia:

```text
/home/linux/
├── documentos/
└── teste.txt
```

Depois foram criados:

```text
/home/linux/
├── documentos/
├── teste.txt
├── docker/
└── projeto/
```

Se o snapshot anterior for restaurado, as alterações realizadas posteriormente poderão ser perdidas.

Por isso, antes de restaurar um snapshot, verifique se existem arquivos ou configurações que precisam ser preservados.

Uma alternativa para preservar o estado atual antes da restauração é criar um novo snapshot.

## Restaurando pelo VBoxManage

A restauração também pode ser realizada pelo terminal:

```powershell
VBoxManage snapshot "debian-lab" restore "Debian inicial"
```

Esse comando restaura a máquina virtual para o snapshot especificado.

O estado atual da VM será substituído pelo estado correspondente ao snapshot.

## Excluindo um Snapshot

Quando um snapshot não for mais necessário, ele pode ser removido.

Na interface gráfica:

1. Abra o Oracle VirtualBox Manager.
2. Selecione `debian-lab`.
3. Acesse `Snapshots`.
4. Selecione o snapshot.
5. Clique em `Delete`.

A exclusão do snapshot não significa que a máquina virtual será restaurada para outro estado.

O objetivo da operação é remover os dados associados ao snapshot e liberar espaço utilizado no armazenamento.

A operação pode levar algum tempo dependendo da quantidade de dados envolvida.

## Excluindo pelo VBoxManage

Para remover um snapshot através do terminal:

```powershell
VBoxManage snapshot "debian-lab" delete "Debian inicial"
```

Depois disso, podemos verificar novamente:

```powershell
VBoxManage snapshot "debian-lab" list
```

## Renomeando e Alterando a Descrição

Também é possível alterar as informações de um snapshot.

Por exemplo:

```powershell
VBoxManage snapshot "debian-lab" edit "Debian inicial" --name="Debian base"
```

Para alterar a descrição:

```powershell
VBoxManage snapshot "debian-lab" edit "Debian base" --description="Estado base do laboratório Debian"
```

Manter nomes e descrições organizados ajuda quando existem vários snapshots.

## Criando uma Sequência de Snapshots

Em um laboratório, podemos criar diferentes pontos de recuperação.

Por exemplo:

```text
debian-lab
│
├── Debian base
│
├── Antes do Docker
│
├── Docker instalado
│
└── Antes do Magento
```

Cada snapshot pode representar uma etapa diferente do laboratório.

Também é possível criar ramificações a partir de snapshots anteriores.

Por exemplo:

```text
Debian base
    |
    +---- Docker
    |       |
    |       +---- Teste A
    |
    +---- Nginx
            |
            +---- Teste B
```

Esse tipo de estrutura pode ser útil para experimentos diferentes utilizando a mesma máquina virtual como ponto de partida.

## Exemplo Prático

Vamos utilizar o laboratório `debian-lab`.

### Estado inicial

A máquina possui:

```text
Sistema:
Debian

RAM:
2048 MB

CPU:
2

Disco:
20 GB

Rede:
NAT

Guest Additions:
Instalado

Pasta compartilhada:
shared
```

### Criar o ponto de recuperação

Crie:

```text
Nome:
Debian base

Descrição:
Estado base do laboratório após configuração inicial.
```

### Realizar uma alteração

Agora imagine que vamos instalar um novo software:

```bash
sudo apt update
sudo apt install curl
```

Depois podemos realizar outros testes ou alterações.

Se alguma alteração futura causar problemas, o snapshot `Debian base` poderá ser utilizado para retornar ao estado anterior.

## Verificando o Estado Depois da Restauração

Depois de restaurar um snapshot, podemos verificar o sistema novamente.

```bash
cat /etc/os-release
```

Verificar o hostname:

```bash
hostname
```

Verificar a rede:

```bash
ip addr
```

Verificar o armazenamento:

```bash
lsblk
```

Verificar a memória:

```bash
free -h
```

Verificar a quantidade de CPUs:

```bash
nproc
```

Esses comandos permitem confirmar que a máquina voltou ao estado esperado.

## Boas Práticas

### Utilize nomes descritivos

Evite nomes genéricos como:

```text
snapshot1
teste
novo
backup
```

Prefira nomes que indiquem claramente o estado da máquina:

```text
Debian base
Antes do Docker
Docker instalado
Antes do Magento
```

### Utilize descrições

Uma descrição ajuda a lembrar por que o snapshot foi criado.

Exemplo:

```text
Estado base do laboratório antes da instalação do Docker.
Rede NAT configurada e pasta compartilhada funcionando.
```

### Não acumule snapshots sem necessidade

Snapshots ocupam espaço no armazenamento do host.

Quanto mais alterações forem realizadas depois da criação de um snapshot, maior pode ser o espaço utilizado pelas imagens diferenciais.

Por isso, snapshots antigos que não possuem mais utilidade devem ser avaliados e removidos.

### Não utilize snapshots como backup

Dados importantes devem possuir uma estratégia de backup independente.

O snapshot deve ser tratado como uma ferramenta de laboratório e recuperação rápida de estados da VM.

### Cuidado antes de restaurar

Sempre verifique o estado atual da VM antes de restaurar um snapshot.

Arquivos, instalações e configurações realizadas depois do snapshot podem ser perdidos.

## Resumo

Neste laboratório foram apresentados os principais conceitos relacionados aos snapshots do Oracle VirtualBox.

O fluxo básico pode ser representado da seguinte forma:

```text
Criar VM
   |
   v
Instalar Debian
   |
   v
Configurar rede
   |
   v
Configurar pasta compartilhada
   |
   v
Criar snapshot
   |
   v
Realizar testes
   |
   +---- Tudo funcionando
   |         |
   |         v
   |      Continuar
   |
   +---- Problema
             |
             v
        Restaurar snapshot
```

Os principais comandos utilizados foram:

```powershell
VBoxManage snapshot "debian-lab" list
```

```powershell
VBoxManage snapshot "debian-lab" take "Debian base"
```

```powershell
VBoxManage snapshot "debian-lab" restore "Debian base"
```

```powershell
VBoxManage snapshot "debian-lab" delete "Debian base"
```

## Resultado

Ao finalizar esta etapa, o laboratório possui os principais recursos necessários para trabalhar com uma máquina virtual Debian no Oracle VirtualBox:

```text
Windows
   |
   +-- Oracle VirtualBox
           |
           +-- debian-lab
                   |
                   +-- Debian
                   +-- CPU
                   +-- RAM
                   +-- Disco virtual
                   +-- Rede NAT
                   +-- Guest Additions
                   +-- Pasta compartilhada
                   +-- Snapshots
```

A máquina virtual agora pode ser utilizada como um ambiente de laboratório para estudos de Linux, redes, infraestrutura, Docker e DevOps.

## Considerações

Snapshots são especialmente úteis em ambientes de estudo porque permitem experimentar novas configurações com maior segurança e retornar rapidamente a um estado conhecido da máquina virtual.

Entretanto, eles não substituem uma estratégia de backup.

Também é importante considerar o espaço disponível no computador host e evitar manter uma quantidade desnecessária de snapshots.

Com essa etapa concluída, a documentação do laboratório Windows cobre desde a instalação do VirtualBox até a criação, configuração, utilização e recuperação da máquina virtual.

## Próxima etapa

A documentação Windows deste laboratório foi concluída.

A próxima etapa do projeto será a criação da documentação para ambientes Linux.

A estrutura continuará seguindo a mesma abordagem prática, utilizando máquinas virtuais para estudar Linux, infraestrutura, redes e DevOps.

## Referências

* Oracle VirtualBox 7.2 User Guide
  https://docs.oracle.com/en/virtualization/virtualbox/7.2/user/

* Oracle VirtualBox 7.2 - Working with Virtual Machines
  https://docs.oracle.com/en/virtualization/virtualbox/7.2/user/working-with-vms.html

* Oracle VirtualBox 7.2 - VBoxManage
  https://docs.oracle.com/en/virtualization/virtualbox/7.2/user/vboxmanage.html

