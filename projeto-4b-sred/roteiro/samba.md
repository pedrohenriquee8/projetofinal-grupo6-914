[◀️ Retorne para o serviço Gateway](https://github.com/pedrohenriquee8/projetofinal-grupo6-914/blob/main/projeto-4b-sred/roteiro/gateway.md)

# Criando um Servidor Samba

Samba é um servidor de arquivos que permite aos usuários compartilhar arquivos em um ambiente Linux e Windows.

## Pré-instalação

Para melhor identificação da máquina, altere o nome do hostname para _samba_ ou alguma variação. Para isso, use o seguinte comando no terminal:

```
hostnamectl set-hostname samba
```

Após o comando, verifique se o hostname foi alterado com o comando `hostname`

<div align="center">
<p>Figura 1 - Hostname da máquina.</p>
<img src="../images/samba/hostname_smb.png" />
</div>

## Passo 1: Instalar o Servidor Samba

Você precisará instalar o pacote samba no servidor. Para fazer isso, vá para o terminal e digite:

```
sudo apt install samba
```

Verifique se o samba foi instalado corretamente com o seguinte comando:

```
whereis samba
```

<div align="center"> 
<p>Figura 2 - Verificando instalação do samba.</p>
<img src="../images/samba/whereis-samba.png" />
</div>

## Passo 2: Configurar o arquivo smb.conf

Antes de configurar, faça o backup do arquivo de configuração do samba. Utilize os comandos:

```
sudo cp /etc/samba/smb.conf{,.backup}
sudo bash -c 'grep -v -E "^#|^;" /etc/samba/smb.conf.backup | grep . > /etc/samba/smb.conf'
```

<div align="center"> 
<p>Figura 3 - Backup do arquivo smb.conf.</p>
<img src="../images/samba/backup-conf-samba-2.png" />
</div>

Agora que o servidor Samba está instalado, você precisará configurar o arquivo smb.conf. Este arquivo contém as configurações de compartilhamento de arquivos para o servidor.

Para isso, você pode usar o nano para editar o arquivo `smb.conf`.

```
sudo nano /etc/samba/smb.conf
```

<div align="center">
<p>Figura 4 - Configurando o arquivo smb.conf.</p>
<img src="../images/samba/samba_conf.png" />
</div>

Reinicie o servidor samba com o comando:

```
sudo systemctl restart smbd
```

<p>Figura 5 - Reiniciando o servidor samba.</p>
<div align="center"><img src="../images/samba/restart-samba.png" />
</div>

## Passo 3: Criar os Usuários de Compartilhamento

Primeiro, crie um usuário para o compartilhamento.

<div align="center"> 
<p>Figura 6 - Criação do usuário aluno.</p>
<img src="../images/samba/add-user-aluno.png" />
</div>

Você precisará criar os usuários que terão acesso aos arquivos compartilhados. Isso pode ser feito com o comando "smbpasswd".

<div align="center"> 
<p>Figura 7 - Garantindo acesso ao usuário aluno.</p>
<img src="../images/samba/aluno-sambashare.png" />
</div>

## Passo 4: Criar os Diretórios Compartilhados

Agora você precisará criar os diretórios que serão compartilhados. Para isso, use o comando "mkDIR".

<div align="center"> 
<p>Figura 8 - Criação do diretório de compartilhamento.</p>
<img src="../images/samba/mkdir-sambashare.png" />
</div>

## Passo 5: Atribuir Permissões de Compartilhamento

Você precisará atribuir as permissões de compartilhamento aos usuários e diretórios criados anteriormente. Para fazer isso, use o comando "chmod".

<div align="center"> 
<p>Figura 9 - Atribuindo permissões de compartilhamento.</p>
<img src="../images/samba/group-sambashare.png" />
</div>

## Passo 6: Testar o Servidor Samba

Abra o explorador de arquivos e coloque o endereço como o ip do servidor samba. Em seguida, logue com o usuário e senha configurados anteriormente no servidor.

<div align="center">
<br>
<p>Figura 10 - Login.</p>
<img src="../images/samba/explorer.png" />
</div>

<div align="center">
<br>
<p>Figura 11 - Acesso aos arquivos.</p>
<img src="../images/samba/explorer-done.png" />
</div>

---

Se tudo foi configurado corretamente, você deve ser capaz de conectar-se ao servidor e compartilhar arquivos. Esperamos que este tutorial tenha lhe ajudado a criar um servidor Samba.

[▶️ Prossiga para o serviço DNS Master](https://github.com/pedrohenriquee8/projetofinal-grupo6-914/blob/main/projeto-4b-sred/roteiro/ns1.md)
