[◀️ Introdução](https://github.com/pedrohenriquee8/projetofinal-grupo6-914)

# Visão Geral

## Objetivo

- Em linhas gerais, a finalidade do projeto consiste na criação de um ambiente de rede virtualizado constituído por quatro máquinas virtuais com o Sistema Operacional Ubuntu Server. Desse modo, a equipe constitui-se por um serviço Gateway, por um serviço SAMBA e pelos servidores DNS Master _(nameserver1)_ e Slave _(nameserver2)_, tudo sendo configurado mediante à [Planilha da Equipe](https://github.com/pedrohenriquee8/projetofinal-grupo6-914/blob/main/projeto-4b-sred/planilha/README.md).

- Diante disso, para acessar os serviços descritos acima, os integrantes devem se conectar, via conexão VPN, por intermédio do software de código aberto e gratuito OpenVPN Client, ao gateway da rede interna LabRedes, localizada no Instituto Federal de Alagoas - Campus Arapiraca, sendo necessário instalar o arquivo _vpn914.labredes.arapiraca.ifal.edu.br_, pois será o responsável por prover o acesso em questão. Em seguida, ao estar vinculado ao gateway da rede interna LabRedes, o usuário, mediante o protocolo SSH, pode integrar-se a um dos servidores da equipe, basta inserir o endereço IP corretamente.

<div align="center">
<p>Figura 1 - Tela inicial do software OpenVPN Client.</p>
<img src="./images/geral/01 - Instalação OpenVPN.png" />
</div>

<div align="center">
<p>Figura 2 - Importar arquivo .ovpn para o OpenVPN Client. </p>
<img src="./images/geral/01.1 - Importar arquivo.png" />
</div>

<div align="center">
<p>Figura 3 - Editando arquivo .ovpn para o OpenVPN Client. </p>
<img src="./images/geral/02 - Editando arquivo.png" />
</div>

- Outrossim, para conectar-se aos serviços da equipe, o usuário deve utilizar o software de código aberto e gratuito PuTTY, que é um cliente SSH e Telnet para Windows. Desse modo, o usuário deve inserir o endereço IP do servidor desejado e, em seguida, clicar em _Open_.

<div align="center">
<p>Figura 4 - Tela inicial do software PuTTY.</p>
<img src="./images/geral/03 - Tela inicial PuTTY.png" />
</div>
