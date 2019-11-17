# Tutorial

Uma das coisas que torna seguro o sistema operacional GNU/Linux (na verdade, qualquer sistema baseado no Unix), é a sua exigência de que cada coisa tenha dono e permissões de uso [site](https://tiagotgv.github.io/introducao-ao-unix/).
<br/>

Por que criar usuários no GNU/Linux? Criar uma conta para cada usuário no sistema operacional não serve apenas para restringir ou permitir o acesso aos recursos oferecidos, mas também para respeitar o espaço que cada pessoa tem. Com uma conta, uma pessoa poderá ter os seus próprios diretórios, personalizar o seu desktop, ter atalhos e configurações para os seus programas preferidos, entre outros.<br/>

Além disso, mesmo que o computador onde o GNU/Linux está instalado seja usado apenas por uma pessoa, é recomendável criar um usuário próprio para ela.<br/>

Mas, por qual motivo, se o sistema já conta com um usuário nativo, o root? O usuário root é o que "manda" no sistema, pois ele tem poderes de administrador, o que significa que ele tem acesso a todos os recursos do sistema operacional. Usá-lo no dia-a-dia não é recomendável, pois se o computador for tomado por outra pessoa ou se o próprio usuário fizer alguma coisa errada, o sistema operacional poderá ser seriamente comprometido. 


## Comandos:

+ useradd: Comando utilizado para criação de um usuário.

+ userdel: Comando utilizado para remoção de um usuário.

+ usermod: Comando usado para modificar os dados de um usuário.

+ passwd: Comando usado para definir e ou modificar a senha de um usuário.

+ groupadd: Comando usado para criar um grupo.

+ groupdel: Comando usado para remover um grupo.

+ groupmod: Comando usado para modificar os dados de um grupo.

CRIANDO UM USUÁRIO
Para que seja possível logar no sistema o usuário deverá ter um username (login) e uma senha (password). Para que isso seja possível usaremos os comandos "useradd" e "passwd". Abaixo explicarei como é a sintaxe dos comandos e suas opções:

# COMANDO USERADD
Sintaxe: useradd [opções] <username>

Opções:
-d - Caminho do diretório home do usuário.

-g - Especifica o grupo do usuário.

-c - Inclui um comentário referente ao usuário, tais como nome, setor, etc

-s - Especifica o shell de comando que o usuário irá utilizar.

-m - Cria o diretório home do usuário e copia os arquivos de /etc/skel/ para o home criado (diretório onde se encontram os arquivos default do usuário). Em algumas distribuições não há necessidade de incluirmos essa opção para a criação do home, mas para evitarmos não o criarmos é bom acostumarmos a colocá-la na criação do usuário.

-p - Essa opção serve para especificarmos uma senha já criptografada para o usuário.


$ useradd -g admin -s /bin/bash -d /home/sup1 -c "Usuário Administrativo de Suporte 1" -m sup1

No exemplo acima criamos o usuário sup1, que tem como grupo admin, usando o shell /bin/bash, o home criado foi o /home/sup1 e tem o comentário "Usuário Administrativo de Suporte 1".

COMANDO PASSWD
Sintaxe: passwd [opções] <username>

# Opções:

-d - Permite o usuário acessar (logar) o sistema sem senha.

-l - Bloqueia/trava a conta do usuário. O usuário não consegue logar.

-u - Desbloqueia/destrava a contado usuário (bloqueado pela opção "-l").

-S - Mostra o status da senha do usuário.

# Exemplo 1:

passwd sup1
Chaging password for user sup1
New password: [digitar a senha]
Retype new password: [repetir a senha]

Exemplo 2: Nesse exemplo iremos travar a conta do usuário sup1.

passwd -l sup1

Exemplo 3: Vamos agora destravar a conta do usuário sup1:

passwd -u sup1

# COMANDO USERMOD
Sintaxe: usermod [opções] <username>

Opções:

-d - Modifica o caminho do diretório home do usuário.

-g - Modifica o grupo do usuário.

-c - Modifica o comentário referente ao usuário.

-s - Modifica o Shell de comando que o usuário irá utilizar.

-p - Substitui a senha já criptografada do usuário.

# Exemplo 1: Nesse exemplo estamos modificando o grupo e o comentário do usuário sup1 ao mesmo tempo.

$ usermod -g <novoGrupo> -c "<novoComentario>" sup1

COMANDO USERDEL
Sintaxe: userdel [opções] <username>

Opções:
-r - Ao usarmos essa opção o diretório HOME e Mailbox do usuário será removido. É importante ter certeza ao fazer isso, pois muitas vezes é melhor remover apenas o usuário ou até mesmo suspendê-lo mantendo seus arquivos para auditoria.

Exemplo 1: Remover o usuário sem excluir seus arquivos.

userdel sup1

# Exemplo 2: Remover o usuário e seus arquivos

userdel -r sup1

COMANDO GROUPADD
Sintaxe: groupadd [opções] <groupname>

Opção:
-g - Ao usarmos esta opção, podemos especificar o GID do grupo que estamos criando.

# Exemplo 1: Criando um grupo chamado "administracao".

groupadd administracao

Exemplo 2: Criando um grupo chamado oragroup e especificando o GID 1521.

groupadd -g 1521 oragroup

# COMANDO GROUPMOD
Sintaxe: groupmod [opções] <groupname>

Opção:

-g - Ao usarmos esta opção, podemos modificar o GID do grupo.

-n - Para trocarmos o nome do grupo.

Exemplo 1: Modificando o GID do grupo "administracao".

groupmod -g 666 administracao

# Exemplo 2: Modificando o nome do grupo oragroup.

groupadd -n oracle oragroup


# Para saber mais:

$ man userdel

$ man groupdel

$ man deluser

$ man delgroup

* Como retirar um usuário de um grupo?

# gpasswd -d neo diretoria
Removing user neo from group diretoria
* Editando os arquivos /etc/passwd e /etc/shadow

Muitas vezes, ao alterar o arquivo /etc/passwd, simplesmente utilizamos um editor de textos, porém para uma edição segura desse arquivo é recomendado utilizar o comando vipw:

$ vipw
A utilização desse comando bloqueia o /etc/passwd contra outras possíveis alterações e evita a corrupção do arquivo, caso outra pessoa também esteja mexendo. O editor de textos utilizado será o que está configurado na variável de ambiente EDITOR ou VISUAL; caso as variáveis não estejam configuradas, o vi será utilizado. Para editar o /etc/shadow de forma segura, basta utilizar o comando vipw com a opção -s:

$ vipw -s
* Editando o arquivo /etc/group

Para evitar outras possíveis alterações enquanto é realizada uma edição no arquivo /etc/group, é possível utilizar o comando vigr. Assim como no comando vipw, o editor de textos utilizado será o configurado na variável de ambiente EDITOR ou VISUAL; caso as variáveis não estejam configuradas, o vi será utilizado:

$ vigr


------------------------------------------
# Diretório:

/etc/skel - Neste diretório são armazenados arquivos, por padrão ocultos (arquivos que iniciam com um ".") , que são copiados para o diretório HOME do usuário no momento da criação do usuário. Se precisarmos incluir alguma configuração padrão, podemos usar esse diretório para incluir ou até mesmo editar os arquivos existentes e consequentemente fazer o ajuste a suas necessidades.

# Arquivos:
/etc/passwd - Arquivo que contém várias informações sobre o usuário. Ele é utilizado por vários comandos de sistema e aplicações. Antigamente até mesmo as senhas eram armazenadas nele, porém a algum tempo as senhas estão sendo armazenadas em 

/etc/shadow, arquivo que falaremos a seguir. Só o administrador do sistema consegue modificar esse arquivo.

/etc/shadow - Onde estão armazenadas as senhas criptografadas dos usuários, além de outras informações como expiração da senha etc.

/etc/gshadow - Tem a mesma finalidade do /etc/shadow, só que para grupos e não usuários.

/etc/group - É onde se encontram os grupos existentes no sistema. Cada grupo pode estar associado a vários usuários, este arquivo também é responsável por esta associação.

/etc/motd - Esse arquivo contém as informações que serão exibidas após o login do usuário.

/etc/default/useradd e /etc/login.defs - Arquivos onde se encontram as configurações default de criação de usuários. As configurações podem ser diferentes dependendo de cada "distro", umas por exemplo, não há a necessidade da opção "-m" para a criação do diretório HOME do usuário.

------------------------------------


introdução ao unix
==========

nome: Tiago Nunes

##### 1)

- [x] Adicione um usuário com as seguintes características:

* Nome: Camila Silva

* Login: csilva

* diretório home: /home/csilva

* shell padrão: /bin/bash

* senha: mudar@123


Resposta:

```
$ sudo useradd -g contabilidade -s /bin/bash -d /home/csilva -c "Usuário Camila da contabilidade chegando na area!" -m csilva
```
##### 2)

- [x] Verifique:

* se foi adicionado um linha referente a esse usuário no arquivo /etc/passwd e em
/etc/group.

* Se foi criado o diretório /home/csilva

Resposta:

```
$ vipw

$ csilva:x:1001:, /home/csilva
```

##### 3)

- [x] Alterar as seguintes características para o usuário csilva:

* Shell padrão: /bin/sh

* Senha: 123@mudar

* Verifique se o shell padrão foi alterado em /etc/passwd para o usuário csilva

Resposta:
```
$ sudo vipw

$ csilva:x:1001:1002:Usuário Camila da contabilidade chegando na area!:/home/csilva:/bin/sh

$ passwd csilva
Digite a nova senha UNIX:
Redigite a nova senha UNIX: 
passwd: senha atualizada com sucesso
```


##### 4)

Adicione um grupo chamado Contabilidade

```
$ groupadd Contabilidade 

```
##### 5)

Adicione o usuário csilva ao grupo Contabilidade

```
$ groupadd csilva Contabilidade 

```

##### 6)

Exibir os grupos a qual usuário csilva está relacionado

```
$ csilva:x:1001:1002:Usuário Camila da contabilidade chegando na area!:/home/csilva:/bin/bash
```

-----------------------------------------------

Comandos usados:

```
vigr

vipw

su

su csilva

goupadd contabilidade

groupadd contabilidade

useradd -g 1000 csilva

usermod

addgroup csilva contabilidade

grupos do sistema

cat /etc/group | cut -d: -f1

less /etc/group 
```
