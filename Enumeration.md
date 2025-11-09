
Windows AD:

**xfreerdp**

```xfreerdp /u:stephanie /d:corp.com /v:192.168.50.75```

------

**net.exe**

![[Pasted image 20250819093449.png]]

Podemos especificar um usuário para ter mais informações sobre ele.

![[Pasted image 20250819093900.png]]

Com o print acima, identificamos que o `jeffadmin` faz parte do grupo de *Domains Admins* e isso é importante, vamos enumerarar agora os grupos dentro do domínio.

![[Pasted image 20250819094226.png]]

Alguns desses grupos são instalados por [padrão.](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/manage/understand-security-groups)

Por isso vamos enumerar agora alguns grupos específicos.

![[Pasted image 20250819094646.png]]


--- 

Outra maneira de enumerar, é por meio de Classes e chamadas do PowerShell

```[System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain()```


![[Pasted image 20250819161812.png]]

Com isso sabemos que o [[PdcRoleOwner]] é o "DC1.corp.com"



----

### PowerView

Com o powerview, o processo fica um pouco mais simples

![[Pasted image 20250820214932.png]]

Podemos importar ele, e assim facilitar a usabilidade do script.

Utilizando o comando `Get-NetDomain` podemos visualizar informações sobre o domínio.

![[Pasted image 20250820214956.png]]

Também podemos usar `Get-NetUser`

![[Pasted image 20250820215220.png]]

Para fazer um enum mais simples apenas dos usuarios, vamos filtrar

`Get-NetUser | select cn`

![[Pasted image 20250820215853.png]]


![[Pasted image 20250820220113.png]]


![[Pasted image 20250820221723.png]]
![[Pasted image 20250820221746.png]]


Com esse comando, acabamos vendo informações importantes e cruciais na fase de enumeração...


![[Pasted image 20250820222129.png]]



Podemos usar o comando a seguir para identificar qual grupo local temos admistrador.

```shell

Find-LocalAdminAccess

```


![[Pasted image 20250908121435.png]]