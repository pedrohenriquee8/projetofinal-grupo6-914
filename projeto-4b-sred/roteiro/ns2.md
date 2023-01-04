[◀️ Retorne para o serviço DNS Master](https://github.com/pedrohenriquee8/projetofinal-grupo6-914/blob/main/projeto-4b-sred/roteiro/ns1.md)

# Implementando o serviço DNS Slave

## Passo 1: Configurar as interfaces de rede

A princípio, deve-se configurar as interfaces de rede do servidor DNS Slave. Para isso, deve-se executar o comando a seguir e ajustar de acordo com o que é apresentado na imagem abaixo, conforme a [Planilha da Equipe](https://github.com/pedrohenriquee8/projetofinal-grupo6-914/blob/main/projeto-4b-sred/planilha/README.md):

```
sudo nano /etc/netplan/00-installer-config.yaml
```

<div align="center">
<p>Figura 1 - Interfaces de rede para o serviço DNS Slave.</p>
<img src="../images/ns2/01 - Interface de rede ns2.png" />
</div> <br />

Após a configuração, deve-se executar o comando a seguir para aplicar as alterações:

```
sudo netplan apply
```

<div align="center">
<p>Figura 2 - Aplicando as alterações feitas no arquivo.</p>
<img src="../images/ns2/02 - Aplicando as alterações feitas no arquivo.png" />
</div> <br />

Outrossim, para confirmar que a aplicação foi executada com êxito, é fundamental utilizar o comando a seguir para verificar o status das interfaces de rede:

```
ifconfig -a
```

<div align="center">
<p>Figura 3 - Uso do ifconfig -a.</p>
<img src="../images/ns2/03 - Uso do ifconfig.png" />
</div> <br />

## Passo 2: Instalação do software bind9 e verificando seu status

Para instalar o software bind9, deve-se executar o comando a seguir:

```
sudo apt-get install bind9 dnsutils bind9-doc -y
```

<div align="center">
<p>Figura 4 - Instalação do software bind9.</p>
<img src="../images/ns2/04 - Instalação do software bind9.png" />
</div> <br />

Após a instalação, deve-se verificar o status do serviço bind9, para isso, deve-se executar o comando a seguir:

```
sudo systemctl status bind9
```

<div align="center">
<p>Figura 5 - Verificando o status do bind9.</p>
<img src="../images/ns2/05 - Verificando o status do bind9.png" />
</div> <br />

## Passo 3: Configurando o arquivo named.conf.local e verificando seu status

Para a configuração do arquivo named.conf.local e a verificação da sua alteração, deve-se executar os comandos a seguir:

```
sudo nano /etc/bind/named.conf.local
sudo cat /etc/bind/named.conf.local
```

<div align="center">
<p>Figura 6 - Configurando o arquivo named.conf.local.</p>
<img src="../images/ns2/06 - Configurando o arquivo namedconflocal.png" />
</div> <br />

<div align="center">
<p>Figura 7 - Verificando o arquivo named.conf.local.</p>
<img src="../images/ns2/07 - Verificando o arquivo namedconfiglocal.png" />
</div> <br />

Outrossim, é de suma importância realizar a configuração responsável pela checagem do nome e reiniciar o bind9. Para isso, deve-se executar os comandos a seguir:

```
sudo named-checkconf
sudo systemctl restart bind9.service
```

Por fim, o status do bind9 precisa ser verificado. Assim sendo, deve-se executar o comando a seguir:

```
sudo systemctl status bind9
```

<div align="center">
<p>Figura 8 - Verificando o status do bind9.</p>
<img src="../images/ns2/08 - Verificando o status do bind9.png" />
</div> <br />

## Passo 4: Realização de testes dig

<div align="center">
<p>Figura 9 - Teste dig para o ns2.</p>
<img src="../images/ns2/09 - Teste dig para o ns2.png" />
</div> <br />

<div align="center">
<p>Figura 10 - Teste dig para o gateway.</p>
<img src="../images/ns2/10 - Teste dig para o gateway.png" />
</div> <br />

[▶️ Ir para a Introdução](https://github.com/pedrohenriquee8/projetofinal-grupo6-914)
