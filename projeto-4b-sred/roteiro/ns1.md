[◀️ Retorne para o serviço Samba](https://github.com/pedrohenriquee8/projetofinal-grupo6-914/blob/main/projeto-4b-sred/roteiro/samba.md)

# Implementando o serviço DNS Master

## Passo 1: Instalação do software bind9

Antes de iniciar o processo do DNS Master, torna-se necessário instalar o bind9 e verificar o status através dos comandos:

```
sudo apt-get install bind9 dnsutils bind9-doc
sudo systemctl status bind9
```

<div align="center">
<p>Figura 1 - Instalação do software bind9.</p>
<img src="../images/ns1/01 - Instalação do bind9.png" />
</div> <br />

<div align="center">
<p>Figura 2 - Verificação do status do software bind9.</p>
<img src="../images/ns1/02 - Verificação do status do software.png" />
</div> <br />

## Passo 2: Geração do diretório _zones_

Já verificada a situação do bind9, deve-se acessar o diretório _/etc/bind_ a partir do seguinte comando:

```
ls /etc/bind
```

<div align="center">
<p>Figura 3 - Listagem de arquivos do diretório /etc/bind.</p>
<img src="../images/ns1/03 - Listagem dos arquivos.png" />
</div> <br />

Sendo assim, é de suma importância criar o diretório _zones_ para armazenar os arquivos de configuração do DNS Master. Para isso, deve-se executar o seguinte comando:

```
sudo mkdir /etc/bind/zones
```

<div align="center">
<p>Figura 4 - Criação do diretório zones.</p>
<img src="../images/ns1/04 - Criação do diretório.png" />
</div> <br />

Com isso, é fundamental verificar se o diretório foi criado com sucesso. Para isso, deve-se executar o seguinte comando:

```
ls /etc/bind
```

<div align="center">
<p>Figura 5 - Conferindo a criação do diretório zones.</p>
<img src="../images/ns1/05 - Conferindo a criação do diretório.png" />
</div> <br />

A partir da criação do diretório _zones_, pode ser gerada a zona direta e reversa do DNS Master. Para isso, deve-se executar os seguintes comandos respectivamente:

```
sudo cp /etc/bind/db.empty /etc/bind/zones/db.grupo6.turma914.ifalara.local
sudo cp /etc/bind/db.127 /etc/bind/zones/db.10.9.14.rev
```

<div align="center">
<p>Figura 6 - Criação da zona direta.</p>
<img src="../images/ns1/06 - Criação da zona direta.png" />
</div> <br />

<div align="center">
<p>Figura 7 - Criação da zona reversa.</p>
<img src="../images/ns1/07 - Criação da zona reversa.png" />
</div> <br />

Nesse cenário, para os próximos passos, é fundamental utilizar o comando _cd /etc/bind/zones/_ para ser direcionado ao diretório zones e utilizar o comando _ls -la_ para verificar se a zona direta e reversa foram criadas com eficiência.

<div align="center">
<p>Figura 8 - Conferindo a criação das zonas.</p>
<img src="../images/ns1/08 - Conferindo a geração das zonas.png" />
</div> <br />

## Passo 3: Configuração dos arquivos db das zonas direta e reversa

Agora, é necessário configurar os arquivos _db.grupo6.turma914.ifalara.local_ e _db.10.9.14.rev_ para que o DNS Master possa ser configurado de acordo com as imagens a seguir. Para isso, deve-se executar os seguintes comandos:

```
sudo nano db.grupo6.turma914.ifalara.local
sudo nano db.10.9.14.rev
```

<div align="center">
<p>Figura 9 - Editando o arquivo db da zona direta.</p>
<img src="../images/ns1/09 - Editando o arquivo db da zona direta.png" />
</div> <br />

<div align="center">
<p>Figura 10 - Editando o arquivo db da zona reversa.</p>
<img src="../images/ns1/10 - Editando o arquivo db da zona reversa.png" />
</div> <br />

Para conferir tais alterações, utiliza-se o comando cat para verificar o conteúdo dos arquivos _db.grupo6.turma914.ifalara.local_ e _db.10.9.14.rev_.

```
sudo cat db.grupo6.turma914.ifalara.local
sudo cat db.10.9.14.rev
```

<div align="center">
<p>Figura 11 - Conferindo o arquivo db da zona direta.</p>
<img src="../images/ns1/11 -  Conferindo o arquivo db da zona direta.png" />
</div> <br />

<div align="center">
<p>Figura 12 - Conferindo o arquivo db da zona reversa.</p>
<img src="../images/ns1/12 -  Conferindo o arquivo db da zona reversa.png" />
</div> <br />

## Passo 4: Configuração do arquivo named.conf.local

Assim sendo, após a verificação de todos os arquivos db, é necessário retornar ao diretório _/etc/bind_ e editar o arquivo _named.conf.local_ para que o DNS Master possa ser configurado. Para isso, deve-se executar o comando a seguir e inserir as linhas de configuração conforme a imagem a seguir:

```
sudo nano named.conf.local
```

<div align="center">
<p>Figura 13 - Arquivo de configuração named.conf.local.</p>
<img src="../images/ns1/13 - Arquivo de configuração namedconflocal.png" />
</div> <br />

Para conferir tais alterações, utiliza-se o comando cat para verificar o conteúdo do arquivo _named.conf.local_.

```
sudo cat named.conf.local
```

<div align="center">
<p>Figura 14 - Conferindo o arquivo de configuração named.conf.local.</p>
<img src="../images/ns1/14 - Conferindo o arquivo de configuração namedconflocal.png" />
</div> <br />

## Passo 5: Verificação das sintaxes

Com toda a configuração realizada, é fundamental que seja verificada a sintaxe do bind9. Para isso, deve-se executar o comando a seguir:

```
sudo named-checkconf
```

<div align="center">
<p>Figura 15 - Verificando a sintaxe do bind.</p>
<img src="../images/ns1/15 - Verificando a sintaxe do bind.png" />
</div> <br />

Após isso, deve-se prosseguir para o diretório _/etc/bind/zones_ e executar os comandos a seguir para verificar a sintaxe das zonas direta e reversa respectivamente:

```
sudo named-checkzone grupo6.turma914.ifalara.local db.grupo6.turma914.ifalara.local
sudo named-checkzone 14.9.10.in-addr.arpa db.10.9.14.rev
```

<div align="center">
<p>Figura 16 - Verificando a sintaxe da zona direta.</p>
<img src="../images/ns1/16 - Verificando a sintaxe da zona direta.png" />
</div> <br />

<div align="center">
<p>Figura 17 - Verificando a sintaxe da zona reversa.</p>
<img src="../images/ns1/17 - Verificando a sintaxe da zona reversa.png" />
</div> <br />

Outrossim, é necessário realizar a configuração do arquivo _/etc/default/named_. Assim, deve-se ajustar a variável _OPTIONS_ para que o DNS Master possa ser configurado. Para isso, deve-se executar o comando a seguir e inserir a linha de configuração conforme a imagem a seguir:

```
sudo nano /etc/default/named
```

<div align="center">
<p>Figura 18 - Configuração do arquivo /etc/default/named.</p>
<img src="../images/ns1/18 - Configuração do arquivo defaultnamed.png" />
</div> <br />

Feito isso, o bind9 deve ser ativado a partir do comando:

```
sudo systemctl enable bind9
```

## Passo 6: Reinicialização do serviço e verificação do seu status

Após a configuração do DNS Master, é de suma importância reinicializar o serviço e verificar o seu status. Para isso, deve-se executar os comandos a seguir:

```
sudo systemctl restart bind9
sudo systemctl status bind9
```

<div align="center">
<p>Figura 19 - Reinício e verificação do status.</p>
<img src="../images/ns1/19 - Reinício e verificação do status.png" />
</div> <br />

Outrossim, é preciso confirmar o status da interface ens160. Para isso, deve-se executar o comando a seguir:

```
systemd-resolve --status ens160
```

<div align="center">
<p>Figura 20 - Confirmação do status do ens160.</p>
<img src="../images/ns1/20 - Confirmação do status do ens160.png" />
</div> <br />

## Passo 7: Realização de testes dig

<div align="center">
<p>Figura 21 - Teste dig para o ns1.</p>
<img src="../images/ns1/21 -  Teste dig para o ns1.png" />
</div> <br />

<div align="center">
<p>Figura 22 - Teste dig para o ns2.</p>
<img src="../images/ns1/22 - Teste dig para o ns2.png" />
</div> <br />

<div align="center">
<p>Figura 23 - Teste dig para o gateway.</p>
<img src="../images/ns1/23 - Teste dig para o gateway.png" />
</div> <br />

<div align="center">
<p>Figura 24 - Teste dig para o samba.</p>
<img src="../images/ns1/24 - Teste dig para o samba.png" />
</div> <br />

[▶️ Prossiga para o serviço DNS Slave](https://github.com/pedrohenriquee8/projetofinal-grupo6-914/blob/main/projeto-4b-sred/roteiro/ns2.md)
