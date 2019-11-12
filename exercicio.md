# introdução ao unix 

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
