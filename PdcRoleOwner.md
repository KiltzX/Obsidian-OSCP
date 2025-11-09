
No **Active Directory**, cada domínio tem **um único Controlador de Domínio Primário (PDC)**, que é o servidor responsável por manter as informações mais atualizadas e críticas (ex.: mudanças de senha, bloqueios de conta, sincronização de horário etc.).

O **PdcRoleOwner** é a **propriedade que identifica qual DC está desempenhando o papel de PDC** dentro do domínio.

- Todo domínio tem vários **DCs (Domain Controllers)** que replicam informações entre si.
    
- Mas algumas funções só podem ser desempenhadas por um único servidor. Essas funções são chamadas de **FSMO roles** (_Flexible Single Master Operations_).
    
- Uma dessas funções é justamente o **PDC Emulator**, e quem está no controle dessa função é mostrado pelo atributo **PdcRoleOwner**.
    

  

👉 Em resumo:

- **PdcRoleOwner = quem é o “dono” do papel de PDC**.
    
- Serve para descobrir qual servidor tem o papel principal e deve ser consultado quando queremos as informações mais recentes e confiáveis no domínio.
    