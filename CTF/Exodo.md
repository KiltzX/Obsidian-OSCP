Link: https://app.hackingclub.com/training/training-machines/181

*"Máquina sobre Kerberos enumeration, ACL's e Group WriteOwner."*



Durante a fase de enumeração, identifiquei o domínio utilizando o **[[NXC]]** anonymous login

![[Pasted image 20250824153219.png]]

``nxc smb [IP] -u '' -p ''``

A requisição falhou, mas ms respondeu com o nome do domínio

Agora com o [[Kerbrute]] podemos enumerar os usuarios

![[Pasted image 20250824153333.png]]

Chegamos no usuario "juanluna", foi tentado pegar o TGT da senha, mas não conseguimos.

Com isso, foi usado um brute force no usuário, pra tentar um login nele.

![[Pasted image 20250824155111.png]]

Com isso, chegamos que a senha é válida, MAS a senha esta expirada.

Utilizando da ferramenta "changepasswd.py" do impacket, conseguimos alterar a senha desse usuario.

`changepasswd.py 'exodo.hc/juanluna@172.16.13.57' -newpass "T@st3P@ss"`

![[Pasted image 20250824155443.png]]


Agora com esse usuário, vamos enumerar o ldap usando o *[[Bloodhound]]*

`nxc ldap 172.16.13.57 -u 'juanluna' -p 'T@st3P@ss' --bloodhound -c All --dns-server 172.16.13.57

Em resposta ao bloodhound, chegamos no seguinte resultado

![[Pasted image 20250824161334.png]]

Com este nível de acesso, o nosso usuário pode alterar a senha do usuario "svc_spot"


--- 

Alteramos a senha do usuário com o comando abaixo, e validamos usando o nxc
`net rpc password 'svc_spot' 'T@st3P@ss' -U 'exodo.hc'/'juanluna'%'T@st3P@ss' -S exodo.hc`


![[Pasted image 20250824162010.png]]


Agora vamos enumerar o nível de acesso de permissões usando o bloodhound

(Vou continuar a máquina)