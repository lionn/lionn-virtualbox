# Configurando a Rede no Debian

## Introdução

Após instalar o Debian na máquina virtual, o próximo passo é configurar e verificar a conectividade de rede do sistema.

O Oracle VirtualBox fornece uma interface de rede virtual para a máquina `debian-lab`. Neste laboratório será utilizado o modo **NAT**, permitindo que o Debian utilize a conexão de Internet disponível no computador hospedeiro.

Neste documento serão realizados os principais procedimentos para verificar a interface de rede, identificar o endereço IP, testar a conectividade e confirmar o funcionamento da resolução de nomes.

## Objetivo

Ao final deste procedimento, a máquina virtual deverá possuir uma interface de rede funcional e acesso à rede externa.

A estrutura do ambiente será:

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
Oracle VirtualBox
    |
    v
Rede NAT
    |
    v
Debian
```

## Pré-requisitos

Antes de iniciar, é necessário ter:

* Oracle VirtualBox instalado no Windows
* Máquina virtual `debian-lab` criada
* Debian instalado
* Adaptador de rede virtual habilitado
* Máquina virtual configurada para utilizar NAT

A instalação do Debian é apresentada no documento:

```text
docs/windows/04-instalando-o-debian.md
```

## Verificando o adaptador de rede no VirtualBox

Antes de verificar a rede dentro do Debian, confirme se o adaptador de rede da máquina virtual está habilitado.

No Oracle VirtualBox, selecione a máquina virtual `debian-lab` e acesse suas configurações.

Localize a categoria:

```text
Configurações
    |
    +-- Rede
```

O primeiro adaptador deverá estar habilitado.

Para este laboratório será utilizada a seguinte configuração:

```text
Adaptador 1: habilitado
Modo de conexão: NAT
```

O VirtualBox disponibilizará uma interface de rede virtual para o sistema convidado.

## Iniciando o Debian

Inicie a máquina virtual `debian-lab`.

Após o carregamento do Debian, abra um terminal.

Os procedimentos de verificação de rede serão realizados utilizando ferramentas disponíveis no próprio sistema.

## Identificando as interfaces de rede

Para listar as interfaces de rede disponíveis no Debian, utilize:

```bash
ip link
```

O comando exibirá as interfaces de rede reconhecidas pelo sistema.

Um resultado semelhante a este poderá ser apresentado:

```text
1: lo: <LOOPBACK,UP,LOWER_UP> ...
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> ...
```

A interface `lo` corresponde à interface de loopback.

A outra interface representa o adaptador de rede virtual disponibilizado pelo VirtualBox.

O nome da interface pode variar de acordo com a configuração do sistema.

## Identificando o endereço IP

Para verificar os endereços IP atribuídos às interfaces, utilize:

```bash
ip addr
```

Também é possível utilizar uma forma mais direta:

```bash
ip -br addr
```

Um resultado semelhante poderá ser apresentado:

```text
lo        UNKNOWN        127.0.0.1/8
enp0s3    UP             10.0.2.15/24
```

O endereço IP apresentado pode variar.

Quando o modo NAT é utilizado com a configuração padrão do VirtualBox, é comum que a máquina virtual receba um endereço de uma rede privada utilizada pelo próprio VirtualBox.

## Verificando o endereço IPv4

Para visualizar somente as informações relacionadas aos endereços IPv4, pode ser utilizado:

```bash
ip -4 addr
```

O resultado deverá apresentar um endereço IPv4 associado à interface de rede.

Exemplo:

```text
inet 10.0.2.15/24
```

O endereço exato dependerá da configuração da rede virtual.

## Verificando a rota padrão

Além do endereço IP, é necessário verificar se o Debian possui uma rota padrão configurada.

Execute:

```bash
ip route
```

Um resultado semelhante poderá ser apresentado:

```text
default via 10.0.2.2 dev enp0s3
10.0.2.0/24 dev enp0s3 proto kernel scope link src 10.0.2.15
```

A linha iniciada por `default` representa a rota padrão utilizada para alcançar redes externas.

Os endereços apresentados podem variar conforme a configuração da rede.

## Entendendo a rota padrão

A rota padrão informa ao sistema para onde devem ser encaminhados os pacotes destinados a redes que não estão diretamente conectadas à máquina.

Em uma configuração NAT padrão do VirtualBox, o gateway pertence à rede virtual criada pelo próprio VirtualBox.

A estrutura pode ser representada da seguinte forma:

```text
Debian
   |
   | 10.0.2.15
   v
Gateway virtual
   |
   | NAT
   v
Windows
   |
   v
Internet
```

O endereço utilizado pelo gateway não deve ser definido manualmente sem necessidade. Ele normalmente é fornecido automaticamente pela configuração de rede da máquina virtual.

## Testando a conectividade com o gateway

Com o endereço da rota padrão identificado, é possível testar a comunicação com o gateway.

Por exemplo:

```bash
ping -c 4 10.0.2.2
```

Substitua o endereço pelo gateway apresentado pelo comando `ip route`.

Um resultado semelhante poderá ser apresentado:

```text
64 bytes from 10.0.2.2: icmp_seq=1 ttl=64 time=0.XXX ms
64 bytes from 10.0.2.2: icmp_seq=2 ttl=64 time=0.XXX ms
```

O resultado exato depende das condições do ambiente.

O teste confirma que a máquina consegue se comunicar com o gateway da rede virtual.

## Testando a conectividade com a Internet

Depois de verificar o gateway, podemos testar a comunicação com um endereço externo.

Um exemplo é:

```bash
ping -c 4 1.1.1.1
```

Se houver resposta, significa que a máquina virtual possui conectividade IP com uma rede externa.

Exemplo:

```text
64 bytes from 1.1.1.1: icmp_seq=1 ttl=XXX time=XX.X ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=XXX time=XX.X ms
```

A ausência de resposta ao `ping` não significa necessariamente que a Internet esteja indisponível, pois alguns servidores ou redes podem bloquear pacotes ICMP.

Por isso, também será realizado um teste utilizando HTTP e HTTPS.

## Testando o acesso HTTP e HTTPS

Para verificar o acesso a um endereço externo utilizando HTTP ou HTTPS, utilize o comando:

```bash
curl -I https://www.debian.org
```

Se a conexão estiver funcionando, o comando deverá apresentar informações relacionadas à resposta HTTP.

Um resultado semelhante poderá ser:

```text
HTTP/2 200
```

O código de resposta pode variar conforme o servidor e o endereço utilizado.

O importante neste teste é confirmar que o Debian consegue estabelecer uma conexão com um servidor externo utilizando HTTPS.

## Verificando a resolução de nomes

O acesso à Internet normalmente depende da resolução de nomes DNS.

Para testar a resolução de um domínio, utilize:

```bash
getent hosts debian.org
```

Um resultado semelhante poderá ser:

```text
XXX.XXX.XXX.XXX debian.org
```

O endereço IP retornado poderá variar.

Esse teste confirma que o sistema conseguiu resolver o nome `debian.org` para um endereço IP.

## Verificando o DNS

Também é possível verificar as informações utilizadas pelo sistema para resolução de nomes.

Em sistemas Debian que utilizam `systemd-resolved`, pode ser utilizado:

```bash
resolvectl status
```

Caso o comando não esteja disponível ou o sistema utilize outro mecanismo de resolução, a configuração poderá ser verificada por outros meios.

O arquivo tradicional relacionado à configuração de resolução de nomes é:

```text
/etc/resolv.conf
```

Seu conteúdo pode ser consultado utilizando:

```bash
cat /etc/resolv.conf
```

A forma como esse arquivo é gerenciado pode variar de acordo com a configuração do Debian.

## Testando a resolução de nomes com ping

Outra forma simples de verificar a resolução DNS é utilizar um domínio diretamente no comando `ping`.

Por exemplo:

```bash
ping -c 4 debian.org
```

Se o nome for resolvido corretamente, o comando exibirá o endereço IP utilizado pelo destino.

Exemplo:

```text
PING debian.org (XXX.XXX.XXX.XXX) ...
```

Nesse caso, além da conectividade, também estará sendo testada a resolução do nome.

## Verificando o estado da interface

Para verificar rapidamente o estado das interfaces e seus endereços, utilize:

```bash
ip -br addr
```

Um resultado esperado poderá ser semelhante a:

```text
lo        UNKNOWN        127.0.0.1/8
enp0s3    UP             10.0.2.15/24
```

A interface utilizada pela máquina deverá aparecer como `UP`.

O nome da interface e o endereço IP podem ser diferentes no ambiente utilizado.

## Obtendo informações detalhadas da interface

Para visualizar informações mais detalhadas sobre uma interface específica, utilize:

```bash
ip addr show enp0s3
```

Substitua `enp0s3` pelo nome da interface apresentado no seu sistema.

O resultado poderá apresentar informações como:

```text
state UP
inet 10.0.2.15/24
```

Essas informações permitem confirmar se a interface está ativa e qual endereço foi atribuído a ela.

## Verificando a conectividade em etapas

Uma forma simples de diagnosticar problemas de rede é testar a comunicação em diferentes níveis.

A sequência pode ser:

```text
1. Interface de rede
       |
       v
2. Endereço IP
       |
       v
3. Gateway
       |
       v
4. Internet por IP
       |
       v
5. Resolução DNS
       |
       v
6. Acesso HTTPS
```

Essa abordagem facilita a identificação da origem de um problema.

Por exemplo, se a interface estiver sem endereço IP, não faz sentido começar investigando DNS.

## Teste completo

Depois de realizar as verificações anteriores, podemos executar uma sequência simples de testes.

Verificar as interfaces:

```bash
ip -br addr
```

Verificar a rota:

```bash
ip route
```

Testar um endereço IP externo:

```bash
ping -c 4 1.1.1.1
```

Testar a resolução de nomes:

```bash
getent hosts debian.org
```

Testar uma conexão HTTPS:

```bash
curl -I https://www.debian.org
```

Se os testes forem concluídos corretamente, teremos uma indicação de que a conectividade de rede está funcionando.

## Configuração utilizada

A configuração de rede utilizada neste laboratório será:

| Recurso         | Configuração           |
| --------------- | ---------------------- |
| Adaptador       | Adaptador 1            |
| Estado          | Habilitado             |
| Modo de conexão | NAT                    |
| Endereço IP     | Obtido automaticamente |
| Gateway         | Obtido automaticamente |
| DNS             | Obtido automaticamente |

Os endereços IP, gateway e servidores DNS podem variar de acordo com o ambiente utilizado.

## Resultado

Após concluir este procedimento, a máquina virtual `debian-lab` deverá possuir conectividade de rede funcional.

A estrutura do laboratório será:

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
Oracle VirtualBox
    |
    v
NAT
    |
    v
Debian
    |
    +-- Interface de rede
    |
    +-- Endereço IP
    |
    +-- Gateway
    |
    +-- DNS
```

O Debian estará apto a acessar repositórios, realizar atualizações e baixar pacotes necessários para os próximos procedimentos do laboratório.

## Considerações finais

A configuração de rede é uma das etapas fundamentais na preparação de um ambiente Linux.

Neste laboratório foi utilizado o modo NAT do Oracle VirtualBox por ser uma configuração simples e adequada para uma máquina virtual destinada inicialmente a estudos.

Durante o procedimento foram verificadas a interface de rede, o endereço IP, a rota padrão, a conectividade externa e a resolução de nomes.

Essa abordagem também fornece uma base para diagnosticar problemas de conectividade em ambientes Linux.

Em laboratórios mais avançados, outros modos de rede do VirtualBox poderão ser utilizados de acordo com a necessidade, como Bridge, Host-only ou redes internas.

## Próxima etapa

Com a rede configurada e funcionando, o próximo procedimento será configurar uma pasta compartilhada entre o Windows e o Debian.

O objetivo será permitir a troca de arquivos entre o sistema hospedeiro e a máquina virtual.

O procedimento será documentado em:

```text
docs/windows/06-pastas-compartilhadas.md
```

