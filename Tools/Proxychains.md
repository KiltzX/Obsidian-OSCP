
Abre a porta para fazer o proxy

```

ssh -D 1080 -C -N -p 22 Eric.Wallows@192.168.218.147

```


client do mssql com o impacket
```

 proxychains impacket-mssqlclient sql_svc:Dolphin1@10.10.178.148 -windows-auth

```

