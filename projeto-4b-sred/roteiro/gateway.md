[◀️ Retorne para o guia do Roteiro](https://github.com/pedrohenriquee8/projetofinal-grupo6-914/blob/main/projeto-4b-sred/roteiro/README.md)

# Implementando o serviço Gateway

O servidor de gateway pode, através do NAT (Network Address Translation), realizar o roteamento de todas as máquinas virtuais da rede interna, ou seja, dos serviços implementados pela equipe, como o SAMBA, DNS Master e DNS Slave, para uma rede externa, como a Internet, utilizando um endereço de saída.

## Entrada ao Gateway

Para conectar-se, faz-se necessário que o usuário tenha acesso ao PuTTY, que é um software de terminal que permite a conexão remota com um servidor. Com isso, basta inserir o endereço da máquina virtual que corresponde ao gateway da equipe e ingressar no terminal.

<div align="center">
<p>Figura 1 - Entrada ao Gateway via PuTTY.</p>
<img src="../images/gateway/01 - Entrada ao Gateway.png" />
</div>

## Definição do Hostname

Para melhor identificação da máquina virtual responsável pelo gateway, é de suma importância definir o nome do hostname para o que está de acordo com a [Planilha da Equipe](https://github.com/pedrohenriquee8/projetofinal-grupo6-914/blob/main/projeto-4b-sred/planilha/README.md). Para isso, deve-se usar o comando abaixo no terminal e conferir se a alteração foi feita com sucesso:

```
hostnamectl set-hostname gw.grupo6.turma914.ifalara.local
```

<div align="center">
<p>Figura 2 - Conferindo o hostname do gateway.</p>
<img src="../images/gateway/02 - Conferindo o hostname.png" />
</div>

## Passo 1: Configuração do Firewall

Para um servidor gateway, é necessário que o firewall esteja configurado para permitir o acesso externo aos serviços implementados pela equipe. Logo, com o intuito de habilitar o firewall e permitir o acesso ssh, utiliza-se o seguinte comando:

```
sudo ufw enable
sudo ufw allow ssh
```

<div align="center">
<p>Figura 3 - Configurando o Firewall do gateway.</p>
<img src="../images/gateway/03 - Configurando o Firewall.png" />
</div>

## Passo 2: Habilitar o encaminhamento de pacotes da interface WAN para a LAN e verificar as interfaces de rede

Para que o gateway possa encaminhar os pacotes da interface WAN para a LAN, é necessário que o encaminhamento de pacotes esteja habilitado. Para isso, utiliza-se o comando abaixo e descomenta a linha que contém o parâmetro _net/ipv4/ip_forward=1_:

```
sudo nano /etc/ufw/sysctl.conf
```

<div align="center">
<p>Figura 4 - Parâmetro do arquivo sysctl.conf descomentado.</p>
<img src="../images/gateway/04 - Parâmetro arquivo sysctl.png" />
</div> <br />

Outrossim, faz-se necessário configurar a interface de rede netplan, em que deve estar de acordo com a [Planilha da Equipe](https://github.com/pedrohenriquee8/projetofinal-grupo6-914/blob/main/projeto-4b-sred/planilha/README.md). Nesse sentido, para tal aplicação, utiliza-se o comando abaixo:

```
sudo nano /etc/netplan/00-installer-config.yaml
```

<div align="center">
<p>Figura 5 - Acesso ao arquivo 00-installer-config.yaml.</p>
<img src="../images/gateway/05 - Arquivo com as interfaces de rede.png " />
</div> <br />

Desse modo, com o arquivo sendo configurado corretamente, basta o integrante inserir o comando a seguir. Além disso, é válido salientar que a interface ens160 é a responsável pela rede WAN, já a ens192 é pela rede LAN.

```
sudo netplan apply
```

<div align="center">
<p>Figura 6 - Uso do comando ifconfig -a para a visualização das interfaces de rede.</p>
<img src="../images/gateway/06 - Configuração da interface de rede netplan.png" />
</div>

## Passo 3: Configuração do arquivo _/etc/rc.local_.

O arquivo _/etc/rc.local_ é um script em que deve ser instruido ao Linux tudo aquilo que necessita ser executado logo após iniciar todos os serviços, ou seja, após o boot do sistema. Para isso, utiliza-se o comando abaixo para a sua criação:

```
sudo nano /etc/rc.local
```

Assim sendo, dentro do arquivo, é de suma importância que seja inserido um conjunto de políticas de roteamento, como pode ser visto na imagem abaixo:

<div align="center">
<p>Figura 7 - Interior do arquivo /etc/rc.local.</p>
<img src="../images/gateway/07 - Configuração do arquivo rclocal.png" />
</div> <br />

Com toda a configuração concluída, é essencial tornar o arquivo executável e inicializável no boot, além de verificar se o firewall está funcionando. Para isso, utiliza-se os seguintes comandos:

```
sudo chmod 755 /etc/rc.local
sudo ufw status
```

<div align="center">
<p>Figura 8 - Listando o arquivo /etc/rc.local.</p>
<img src="../images/gateway/08 - Listando o arquivo rclocal.png" />
</div> <br />

<div align="center">
<p>Figura 9 - Comandos para o arquivo /etc/rc.local.</p>
<img src="../images/gateway/09 - Comandos para o arquivo rclocal.png" />
</div> <br />

Outrossim, para que ocorra a recepção e o encaminhamento de pacotes com o servidor Samba, ou seja, disponibilizar o serviço do compartilhamento de arquivos externamente, é de suma importância adicionar certos parâmetros, como pode ser visto na imagem abaixo:

<div align="center">
<p>Figura 10 - Parâmetros que disponibilizam o serviço de compartilhamento de arquivos externamente (SAMBA).</p>
<img src="../images/gateway/10 - Configurando para a entrada de pacotes [Samba].png" />
</div> <br />

Por fim, também será feito o mesmo procedimento para a interface DNS Master, ou seja, para que o servidor possa receber e encaminhar pacotes externamente. Assim, pode-se visualizar na imagem abaixo os parâmetros que devem ser adicionados:

<div align="center">
<p>Figura 11 - Parâmetros que disponibilizam o serviço de compartilhamento de arquivos externamente (DNS Master).</p>
<img src="../images/gateway/11 - Configurando o arquivo rclocal para a recepção de pacotes com base no servidor DNS Master.png" />
</div>

<hr />

## Conclusão

Nesse cenário, seguindo os procedimentos descritos, o gateway estará pronto para receber e encaminhar pacotes externos, desde a ativação do firewall até a configuração do arquivo _/etc/rc.local_ para a recepção e encaminhamento de pacotes com o servidor Samba e com o servidor DNS Master.

Portanto, para prosseguir com o processo de configuração dos serviços, clique no link abaixo e confira o passo a passo para a instalação do servidor Samba.

[▶️ Prossiga para o servidor Samba](https://github.com/pedrohenriquee8/projetofinal-grupo6-914/blob/main/projeto-4b-sred/roteiro/samba.md)
