# GLPI - 9.5.12 com aaPanel - Painel Administrativo



![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-12-20-41-image.png)



### Procedimentos aplicados durante instalação do **GLPI - 9.5.12**.



Segui abaixo os requisitos mínimos para Host da aplicação GLPI em produção:



##### Configurações de Hardware necessário

**Requisitos:**

- 2 GB - RAM;

- 1 Core;

- Disco rígido - **160 GB**;

- Internet;

- Escolher host **virtualizado** ou **físico**;
  
  

#### Software necessários

- **Ubuntu Server 20.04;**

- **Apache 2.2;**

- **PHP  7.4;**

- **Mysql 5.x** ou **MariaDB 10.x;**

- Aplicativo para acessar o banco: **phpMyAdmin** ou equivalente;

- Serviço **FTP**,  use o **Filezilla, winSCP** ou equivalente;

- Serviço **SSH** será mega necessário, use o **Terminal ou Putty** ou **Bitvise.**



Com a finalidade de ser mais direto ao ponto, não vou explicar como instalar o Ubuntu Server, mas basicamente é uma instalação padrão, onde deixa somente o acesso **SSH** ativado para acessar o host.

#### Dicas Pós-Instalação Ubuntu:

- Anote hostname, usuário padrão e root(lembrando que no ubuntu o root fica sem senha definida);
  
  ![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-15-35-47-image.png)

- Anote o IP do host e porta de serviço(22);



Para facilitar e dar mais agilidade na implementação e instalação, vamos usar o AAPanel. É um **painel administrativo Open Source** de hospedagens de websites, nele tem a uma suite com todas as aplicações necessárias, bibliotecas e scripts necessários para ter uma administração ágil, fácil de instalação e com diversas ferramentas para o dia a dia.



![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-12-42-46-image.png)



## Instalação do aaPanel no Ubuntu 20.04



Atualize primeirament o repositório do Ubuntu:

```
sudo apt update -y
```

Segundoo, olhe se tem algum upgrade no Ubuntu:

```
sudo apt upgrade -y
```

Ao ter instalado o Ubuntu e atualizado tudo, faça o acesso pelo serviço **SSH** para ter melhor usabilidade no acesso. Com permissão de root ou sudo, copie o comando do campo Ubuntu/Deepin como está no site e cole no terminal para ser executado a instalação.

```
wget -O install.sh http://www.aapanel.com/script/install-ubuntu_6.0_en.sh && sudo bash install.sh aapanel
```



![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-15-36-58-image.png)



O script irá perguntar se quer instalar o aaPanel no diretório /www, digite: **y**



Em seguinda, irá pergungar se quer habilitar o SSL, ou melhor, certificado de segurança SSL, digite y caso já queira habilitar, no meu caso não habilitar.

![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-15-38-17-image.png)



No final o script do instalou irá para na seguinte tela.

![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-15-41-28-image.png)



Acessar conforme está na sua tela (instalação), no meu caso  vou digite o seguinte endereço no navegador: http://192.168.18.48:7800/ebe82842

**username:** jzmvfwpq

**password:** 539b82e6



Esses parâmetros de acessos, poderam ser alterado logo depois de você acessar o panel.



Ao logar, irá deparar com a seguinte tela.

<img title="" src="file:///C:/Users/Dirceu%20Vaz/AppData/Roaming/marktext/images/2023-07-16-15-45-40-image.png" alt="" width="709">

Iremos instalar a **versão LAMP**, conforme a imagem.

Certifica-se de escolher a versão do **Apache, MariaDB, PHP** e os demais, conforme os requísitos exigem.



Seguinda irá para seguinte tela, aguarde a instalação. Pode demorar dependendo da configuração do seu host.



![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-15-47-48-image.png)



Terminado a instalação, vai ficar nesta tela.



![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-16-21-04-image.png)



Recomendo reiniciar apesar que no linux não reiniciar.

![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-16-22-03-image.png)

![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-16-22-18-image.png)



![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-16-22-35-image.png)

![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-16-22-52-image.png)



Logue novamente no painel pelo navegador e deixa aberto. Agora vai ho terminal e instale o pacote **openntpd** para ajuster horários e sincronizar região, data e horas.

```
apt install -y openntpd
```



Agora desative o serviço openntpd

```
systemctl stop openntpd
```



Configure o timezone para sua região

```
`dpkg-reconfigure tzdata`
```

![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-16-41-03-image.png)

![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-16-41-17-image.png)



Adicionar **servidor NTP.BR**

```
echo "servers pool.ntp.br" > /etc/openntpd/ntpd.conf
```

Habilitar e Iniciar Serviço **OpenNTPD**

```
systemctl enable openntpd
```

```
systemctl start openntpd
```

Instale os seguinte pacotes para manipulação de pacote

```
apt install -y xz-utils bzip2 unzip curl
```

Agora pacotes relacionado com PHP e Apache:



```
apt install libapache2-mod-php php-soap php-cas php php-{apcu,cli,common,curl,gd,imap,ldap,mysql,xmlrpc,xml,mbstring,bcmath,intl,zip,bz2}
```

Também estes outros pacotes:

```
apt-get install php-cli php-cas php-imap php-ldap php-xmlrpc php-soap php-snmp php-apcu -y
```





![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-16-44-40-image.png)



Apos instalar,o terminal deve apresentar algum erro, ignore. Vá no painel pelo navegador e siga a imagem abaixo, ou reinicie o servidor

```
sudo systemctl reboot
```

Ou siga pelo painel nas imagens abaixas:



![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-16-47-56-image.png)



![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-16-48-37-image.png)

![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-16-49-25-image.png)



Após desativa e reativar o Apache pelo panel, faz igualmente com PHP.

![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-16-50-39-image.png)

![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-16-51-05-image.png)



O GLPI exige as seguintes versões do PHP, segundo a documentação:

https://glpi-install.readthedocs.io/bg/latest/prerequisites.html



![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-16-54-57-image.png)

As extension habilitadas ou instaladas.

- dom
- fileinfo
- filter
- libxml
- json
- simplexml
- xmlreader
- xmlwriter
- curl
- gd
- intl
- mysqli
- session
- zlib
- bz2
- Phar
- zip
- exif`
- ldap
- openssl
- Zend OPcache



Finalmente podemos dizer que podemos iniciar a instalação do GLPI.



### Instalação do GLPI versão 9.5.12.

Faça o download.

Link para download

https://github.com/glpi-project/glpi/releases/

ou

https://github.com/glpi-project/glpi/releases/download/9.5.12/glpi-9.5.12.tgz



No aaPanel é preciso criar um site, vá em Website e clique em addsite.

![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-19-57-37-image.png)



Na imagem abaixo, você irá depará com este formulário para prencher, anote e veja com bastante detalhes.

Em **Domain name**: seu domínio desejado.

Com estou implentando eu um ambiente em rede local, por enquanto será preciso configurar apontamento de DNS. Neste caso é um domínio fictício, irei acessar digite o endereço ip do host, já que o domínio é fictício para o panel administrar.

**FTP:** configure para acessar caso necessário

**Database:** MySQL

**Database settings:** Nome do banco

**Password:** Senha para acessar este banco, não a senha do root do Mysql.

**PHP version:** Para GLPI 9.5.12 é preciso do PHP 7.4.

Caso queria logo ativar SSL, ou melhor, ativar o HTTPS, marque em **SSL** e **HTTP redirect to HTTPS.**



![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-20-03-10-image.png)



Tudo conforme você queria, aperte em **Submit**. Irá para a seguinte tela abaixo.



![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-20-03-25-image.png)

Criado o Website, você poderá ir nos diretórios do site ou aplicação.

![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-20-15-55-image.png)

![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-20-16-23-image.png)

Faça o upload do arquivo compactado do GLPI.

![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-20-17-19-image.png)

![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-20-17-50-image.png)

![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-20-18-27-image.png)



Crie uma pasta para organizar os diretórios e arquivos.



<img src="file:///C:/Users/Dirceu%20Vaz/AppData/Roaming/marktext/images/2023-07-16-20-19-57-image.png" title="" alt="" width="941">

Crei a pasta **BKP**, onde vou deixar somente o arquivo do GLPI compactado e guardar outros  os arquivos dentro da pasta BKP. Caso preferi pode deixar somente os arquivos: **.htaccess** e **.user.ini**.



Clique com botão direio no compactado e clique em **Unzip** para descompactar. Será criada uma pasta com glpi.



![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-20-24-26-image.png)



**Resultado:**

![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-20-27-41-image.png)



Pegue o compactado copie para a pasta BKP e delete o mesmo depois. Agora entre na pasta glpi onde está o script de instalação do GLPI. Selecione todos os arquivos e pasta e copie, conforme a imagem abaixo.



![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-20-29-30-image.png)



Retorne para o diretório do seu domínio, no caso aqui será:

**/www/wwwroot/g9.ecoti.eng.br**



![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-20-30-55-image.png)



Agora delete a pasta **glpi** como a imagem abaixo:



![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-20-31-21-image.png)



Abra uma nova aba no navegador e digite o endereço ip do host que está instalado o panel aaPanel, no caso será **192.168.18.48:8083.**

O navegador irá fazer um requisição no servidor apache, e o apache irá devolver com a página do website que está rodando na porta 8083, sendo assim, você poderá usar diversas vezes, bastante colocar para outra porta disponível.



Agora siga às sequências das imagens para faze a instalação limpa.



![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-20-38-46-image.png)



![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-20-38-27-image.png)

![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-20-39-27-image.png)



Nesta etapa o script informar que precisar ser instalada as extensões do php, vamos isso no panel.



![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-20-40-09-image.png)



No panel siga conforme a imagem abaixo:



![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-20-41-58-image.png)

![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-20-42-38-image.png)



Instale todas as extensões que o script solicitou.



![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-20-47-41-image.png)



Aperte em **Continuar** e Ignore esse Warnning, por o aaPanel já cuida do log.



![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-20-47-14-image.png)



Insirar as informações do banco de dados e aperte Continuar.



![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-20-50-32-image.png)



Marque o nome do seu banco de dados.



![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-20-51-48-image.png)

Na sequencia, siga as imagens.

![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-20-52-30-image.png)

![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-20-52-48-image.png)

![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-20-53-01-image.png)



Aperte em **Usar GLPI** .



![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-20-53-12-image.png)



# Finalmente na Tela inicial do GLPI.

Nesta tela você deverá acessar com as seguintes informações abaixo.

**Digite o usuário padrão:** glpi

**Digite a senha padrão:** glpi



![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-20-54-42-image.png)



## Tela princial com Dashboard e todas as permissões do administrador do GLPI.

![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-20-57-09-image.png)

Vá no diretório onde está instalado o GLPI e remova o script **install.php na pasta install.** E depois altere a senha do administrador.



## Recomendações:

Nunca deverá deletar os usuários padrões do **GLPI**. Somente insirar senhas fortes.

| [glpi](http://192.168.18.48:8083/front/user.form.php?id=2)      |
| --------------------------------------------------------------- |
| [normal](http://192.168.18.48:8083/front/user.form.php?id=5)    |
| [post-only](http://192.168.18.48:8083/front/user.form.php?id=3) |
| [tech](http://192.168.18.48:8083/front/user.form.php?id=4)      |

Faça o registro do seu GLPI no site do desenvolvedor para instalações de plugins.

![](C:\Users\Dirceu%20Vaz\AppData\Roaming\marktext\images\2023-07-16-21-02-05-image.png)

Afinal, e aí gostou desse passo a passo ou tutorial, ou sei lá como queira chamar. Te ajudou a instalar um sistema de Help Desk em sua empresa com a finalidade registrar as suas atividades e indicadores. Espero que sim, qualquer dúvida tô por aí. 



**CONTATO:**

GitHub: https://github.com/dirceuvaz

E-mail: dirceuvaz.dev@gmail.com

Instagram: @dirceu_vaz


