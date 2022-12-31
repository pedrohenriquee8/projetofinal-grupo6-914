

# Criando um Servidor Samba

Samba é um servidor de arquivos que permite aos usuários compartilhar arquivos em um ambiente Linux e Windows. 

## Pré-instalação
Para melhor identificação da máquina, altere o nome do hostname para _samba_ ou alguma variação. Para isso, use o seguinte comando no terminal:

```
hostnamectl set-hostname samba
```

Após o comando, verifique se o hostname foi alterado com o comando `hostname`

Exemplo:

<img src="../images/samba/hostname_smb.png" />

## Passo 1: Instalar o Servidor Samba
Você precisará instalar o pacote samba no servidor. Para fazer isso, vá para o terminal e digite:

```
sudo apt install samba
```

Verifique se o samba foi instalado corretamente com o seguinte comando: 

```
whereis samba
```

Exemplo: 
<img src="../images/samba/whereis-samba.png" />

## Passo 2: Configurar o arquivo smb.conf
Antes de configurar, faça o backup do arquivo de configuração do samba. Utilize os comandos:

```
sudo cp /etc/samba/smb.conf{,.backup}
sudo bash -c 'grep -v -E "^#|^;" /etc/samba/smb.conf.backup | grep . > /etc/samba/smb.conf'
```

Exemplo: 
<img src="../images/samba/backup-conf-samba-2.png" />

Agora que o servidor Samba está instalado, você precisará configurar o arquivo smb.conf. Este arquivo contém as configurações de compartilhamento de arquivos para o servidor.

Para isso, você pode usar o nano para editar o arquivo `smb.conf`.

```
sudo nano /etc/samba/smb.conf
```

Exemplo:
<img src="../images/samba/samba_conf.png" />

Reinicie o servidor samba com o comando:
```
sudo systemctl restart smbd
```

Exemplo
<img src="../images/samba/restart-samba.png" />

## Passo 3: Criar os Usuários de Compartilhamento

Primeiro, crie um usuário para o compartilhamento.

Exemplo: 
<img src="../images/samba/add-user-aluno.png" />

Você precisará criar os usuários que terão acesso aos arquivos compartilhados. Isso pode ser feito com o comando "smbpasswd".

Exemplo: 
<img src="../images/samba/aluno-sambashare.png" />

## Passo 4: Criar os Diretórios Compartilhados
Agora você precisará criar os diretórios que serão compartilhados. Para isso, use o comando "mkDIR".

Exemplo: 
<img src="../images/samba/mkdir-sambashare.png" />

## Passo 5: Atribuir Permissões de Compartilhamento
Você precisará atribuir as permissões de compartilhamento aos usuários e diretórios criados anteriormente. Para fazer isso, use o comando "chmod".

Exemplo: 
<img src="../images/samba/group-sambashare.png" />

## Passo 6: Testar o Servidor Samba

Abra o explorador de arquivos e coloque o endereço como o ip do servidor samba. Em seguida, logue com o usuário e senha configurados anteriormente no servidor.

Login: 
<img src="../images/samba/explorer.png" />

Acesso aos arquivos: 
<img src="../images/samba/explorer-done.png" />

Se tudo foi configurado corretamente, você deve ser capaz de conectar-se ao servidor e compartilhar arquivos.

---

Esperamos que este tutorial tenha lhe ajudado a criar um servidor Samba. 
