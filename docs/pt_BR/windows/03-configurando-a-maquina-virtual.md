# Configurando a Máquina Virtual no Oracle VirtualBox

## Introdução

Após criar a máquina virtual, é necessário revisar e ajustar suas configurações antes de iniciar a instalação do sistema operacional.

O Oracle VirtualBox permite definir diversos recursos de hardware virtual e opções relacionadas ao funcionamento da máquina. Essas configurações determinam como a máquina virtual utilizará os recursos disponíveis no computador físico.

Neste documento serão configurados os principais recursos da máquina virtual `debian-lab`, que será utilizada para instalar o Debian e posteriormente como ambiente de laboratório.

## Objetivo

Ao final deste procedimento, a máquina virtual estará configurada com os recursos necessários para iniciar a instalação do Debian.

A configuração utilizada neste laboratório será:

```text
Máquina virtual: debian-lab
Sistema operacional: Debian
Memória RAM: 2048 MB
Processadores: 2
Disco virtual: 20 GB
Rede: NAT
```

## Acessando as configurações

Abra o Oracle VirtualBox e selecione a máquina virtual `debian-lab`.

Com a máquina virtual desligada, acesse as configurações disponíveis no VirtualBox Manager.

A configuração da máquina é organizada em diferentes categorias, permitindo ajustar os recursos de hardware virtual antes da inicialização.

```text
debian-lab
    |
    +-- Configurações
           |
           +-- Sistema
           +-- Armazenamento
           +-- Rede
           +-- Áudio
           +-- USB
           +-- Outros recursos
```

## Sistema

A categoria **Sistema** reúne configurações relacionadas ao hardware básico da máquina virtual.

Entre os recursos disponíveis estão memória RAM, processadores e ordem de inicialização.

## Memória RAM

A quantidade de memória RAM determina quanto da memória física do computador será disponibilizada para o sistema convidado.

Para este laboratório será utilizada a seguinte configuração:

```text
Memória RAM: 2048 MB
```

A quantidade de memória deve ser definida considerando os recursos disponíveis no computador físico.

Uma configuração muito baixa pode prejudicar o funcionamento do sistema convidado. Por outro lado, reservar memória em excesso pode reduzir os recursos disponíveis para o Windows.

Para um laboratório Debian básico, 2 GB de RAM fornecem uma configuração inicial adequada.

## Processadores

A máquina virtual também pode receber uma quantidade definida de processadores virtuais.

Para este laboratório será utilizado:

```text
Processadores: 2
```

Os processadores virtuais são disponibilizados a partir dos processadores existentes no computador físico.

Assim como acontece com a memória, a quantidade deve ser definida de acordo com os recursos disponíveis no computador hospedeiro.

## Ordem de inicialização

A ordem de inicialização determina quais dispositivos serão consultados pela máquina virtual durante o processo de boot.

Para a instalação do Debian, a máquina deverá utilizar a imagem ISO como mídia de inicialização.

Uma configuração adequada durante a instalação pode ser:

```text
1. Óptico
2. Disco rígido
3. Rede
```

Depois que o Debian estiver instalado, o disco rígido poderá ser utilizado como principal dispositivo de inicialização.

## Armazenamento

A categoria **Armazenamento** apresenta os dispositivos de armazenamento associados à máquina virtual.

Neste laboratório teremos um disco virtual destinado à instalação do Debian.

```text
Controladora
    |
    +-- Disco virtual
           |
           +-- 20 GB
```

O disco virtual será utilizado para armazenar o sistema operacional, seus arquivos e posteriormente os recursos utilizados no laboratório.

## Disco virtual

O disco criado anteriormente possui a seguinte capacidade:

```text
Disco virtual: 20 GB
```

O espaço necessário depende da finalidade da máquina.

Para uma instalação básica do Debian, 20 GB podem ser suficientes. Caso a máquina seja posteriormente utilizada para executar serviços, containers, bancos de dados ou outros projetos, será necessário avaliar a necessidade de armazenamento adicional.

## Mídia de instalação

A imagem ISO do Debian deve estar disponível como mídia de instalação da máquina virtual.

O VirtualBox permite associar uma imagem ISO ao dispositivo óptico virtual.

Durante a instalação, a estrutura será semelhante a:

```text
Máquina virtual
       |
       +-- Controladora de armazenamento
              |
              +-- Disco virtual
              |
              +-- Unidade óptica
                     |
                     +-- debian.iso
```

A imagem ISO será utilizada para inicializar o instalador do Debian.

Após a instalação do sistema, a ISO poderá ser removida da unidade óptica virtual.

## Rede

A configuração de rede determina como a máquina virtual se comunicará com o computador físico e com outras redes.

O VirtualBox disponibiliza diferentes modos de rede, cada um destinado a cenários específicos.

Entre os modos disponíveis estão:

* NAT
* Rede NAT
* Adaptador em modo Bridge
* Rede interna
* Adaptador somente-anfitrião
* Driver genérico

Para este laboratório será utilizado o modo **NAT**.

## Configurando NAT

O modo NAT permite que a máquina virtual utilize a conexão de rede do computador hospedeiro para acessar redes externas.

A estrutura será:

```text
Internet
    |
    v
Roteador
    |
    v
Windows
    |
    v
VirtualBox
    |
    v
Debian
```

A máquina virtual não precisará possuir uma conexão física própria. O VirtualBox realizará a tradução necessária entre a rede virtual e a conexão utilizada pelo computador hospedeiro.

A configuração será:

```text
Adaptador 1: habilitado
Modo de conexão: NAT
```

## Por que utilizar NAT neste laboratório?

O modo NAT é adequado para o primeiro laboratório porque permite que a máquina virtual tenha acesso à rede sem exigir uma configuração adicional no roteador ou na rede física.

Esse modelo é suficiente para tarefas como:

* Atualização do sistema.
* Download de pacotes.
* Acesso a repositórios.
* Navegação na Internet.
* Instalação de ferramentas.
* Testes básicos de conectividade.

Em laboratórios mais avançados, outros modos de rede podem ser utilizados conforme o objetivo do ambiente.

## Adaptador de rede

O VirtualBox disponibiliza uma interface de rede virtual para o sistema convidado.

Para este laboratório será utilizado o adaptador padrão fornecido pelo VirtualBox.

```text
Adaptador 1
    |
    +-- Habilitado
    +-- NAT
    +-- Adaptador padrão
```

A interface será identificada posteriormente pelo Debian e poderá ser consultada utilizando ferramentas como `ip`.

## Áudio

A máquina virtual pode utilizar um dispositivo de áudio virtual.

Como o objetivo deste laboratório é trabalhar com Linux, infraestrutura e servidores, o áudio não é necessário.

A configuração pode permanecer no padrão do VirtualBox ou ser desabilitada para reduzir recursos que não serão utilizados.

Para este laboratório:

```text
Áudio: desabilitado
```

## USB

O VirtualBox permite disponibilizar dispositivos USB do computador físico para a máquina virtual.

Esse recurso pode ser útil em cenários específicos, como testes envolvendo dispositivos externos.

Para este laboratório, não será necessário utilizar dispositivos USB.

A configuração pode permanecer no padrão.

```text
USB: configuração padrão
```

## Tela

A categoria relacionada à tela permite configurar aspectos como memória de vídeo e aceleração gráfica.

Como o objetivo principal desta máquina será executar um ambiente Debian para estudos de infraestrutura, não é necessário utilizar uma configuração gráfica avançada.

Uma configuração básica é suficiente:

```text
Memória de vídeo: configuração padrão
Aceleração 3D: desabilitada
```

Caso a máquina virtual seja utilizada posteriormente para aplicações gráficas, essas configurações poderão ser revistas.

## Pastas compartilhadas

O VirtualBox permite compartilhar diretórios do sistema hospedeiro com a máquina virtual.

Esse recurso pode facilitar a transferência de arquivos entre Windows e Debian.

Neste momento, nenhuma pasta compartilhada será configurada.

```text
Pastas compartilhadas: nenhuma
```

A configuração poderá ser adicionada posteriormente caso exista necessidade de compartilhar arquivos entre os dois sistemas.

## Configurações adicionais

O VirtualBox possui outras opções de configuração relacionadas a recursos específicos da máquina virtual.

Nem todas são necessárias para este laboratório.

A recomendação é manter as opções não utilizadas em seus valores padrão, alterando somente os recursos necessários para o objetivo do ambiente.

Isso também facilita a identificação de problemas caso alguma configuração precise ser revisada posteriormente.

## Configuração final

Depois dos ajustes, a máquina virtual deverá apresentar uma configuração semelhante à seguinte:

```text
Máquina virtual
    |
    +-- Nome
    |     debian-lab
    |
    +-- Sistema
    |     Linux / Debian
    |
    +-- Memória
    |     2048 MB
    |
    +-- Processadores
    |     2
    |
    +-- Armazenamento
    |     20 GB
    |
    +-- Rede
    |     NAT
    |
    +-- Áudio
    |     Desabilitado
    |
    +-- USB
    |     Configuração padrão
    |
    +-- Pastas compartilhadas
          Nenhuma
```

## Revisando a configuração

Antes de iniciar a máquina virtual, revise as principais configurações.

A configuração utilizada neste laboratório será:

| Recurso               | Configuração        |
| --------------------- | ------------------- |
| Nome                  | `debian-lab`        |
| Sistema operacional   | Debian              |
| Memória RAM           | 2048 MB             |
| Processadores         | 2                   |
| Disco virtual         | 20 GB               |
| Rede                  | NAT                 |
| Áudio                 | Desabilitado        |
| USB                   | Configuração padrão |
| Pastas compartilhadas | Nenhuma             |

## Resultado

Após concluir as configurações, a máquina virtual estará preparada para iniciar o processo de instalação do Debian.

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
                            +-- 2 GB RAM
                            +-- 2 CPUs
                            +-- 20 GB Disco
                            +-- NAT
                            +-- Debian ISO
```

Neste momento, o Debian ainda não foi instalado no disco virtual.

A máquina está apenas configurada e pronta para iniciar a instalação do sistema operacional.

## Considerações finais

A configuração adequada dos recursos virtuais é importante para garantir que a máquina convidada tenha recursos suficientes sem comprometer o funcionamento do sistema hospedeiro.

Neste laboratório foi adotada uma configuração simples, adequada para uma instalação inicial do Debian e para os estudos que serão realizados posteriormente.

Os recursos podem ser modificados conforme a finalidade da máquina virtual. Ambientes destinados a Docker, bancos de dados, servidores ou Magento 2, por exemplo, podem exigir mais memória, processadores e armazenamento.

## Próxima etapa

Com a máquina virtual criada e configurada, o próximo procedimento será iniciar a máquina e realizar a instalação do Debian.

O procedimento será documentado em:

```text
docs/windows/04-instalando-o-debian.md
```
