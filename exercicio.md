introdução ao unix 
nome: Tiago Nunes
1. Adicione um usuário com as seguintes características:
• Nome: Camila Silva
• Login: csilva
• diretório home: /home/csilva
• shell padrão: /bin/bash
• senha: mudar@123
R:para esxecutar estas  atividades fizemos o seguinte comondo: sudo useradd -U -p 123 -s /home/csilva csilva

2. Verifique:
• se foi adicionado um linha referente a esse usuário no arquivo /etc/passwd e em
/etc/group.
• Se foi criado o diretório /home/csilva

R: csilva:x:1001:, /home/csilva

3. Alterar as seguintes características para o usuário csilva:
• Shell padrão: /bin/sh
• Senha: 123@mudar
• Verifique se o shell padrão foi alterado em /etc/passwd para o usuário csilva

4. Adicione um grupo chamado Contabilidade

5. Adicione o usuário csilva ao grupo Contabilidade

6. Exibir os grupos a qual usuário csilva está relacionado

7. Ler arquivo 03_-_02 - Passwd e Shadow.pdf e resolver questões. (Enviar respostas em
um arquivo separado)


vigr
vipw
su
su csilva
vipw
su csilva
goupadd contabilidade
groupadd contabilidade
useradd -g 1000 csilva
usermod
addgroup csilva contabilidade
