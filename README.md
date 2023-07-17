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


