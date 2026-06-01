# Caso o Ansible não consiga se conectar ao host Windows usando o protocolo WinRM

## Algumas etapas para tentar resolver o problema

* a. Verifique a conectividade de rede: Primeiro, verifique se há conectividade de rede 
entre a máquina Ansible (de onde você está executando o Ansible) e o host Windows. 
Você pode tentar pingar o host Windows para garantir que a comunicação de rede esteja 
funcionando corretamente.

* b. Confira as configurações de WinRM no host Windows: Certifique-se de que o serviço WinRM 
esteja em execução e configurado corretamente no host Windows. Você pode usar o comando 
winrm quickconfig no PowerShell do Windows para configurar o WinRM.

* c. Verifique as credenciais: Garanta que as credenciais fornecidas no arquivo de 
inventário do Ansible estejam corretas e tenham permissões adequadas para se conectar 
ao host Windows.

* d. Verifique as configurações de firewall: Além de abrir a porta 5985 no firewall do 
Windows, certifique-se de que não há outras configurações de firewall que possam estar 
bloqueando a comunicação entre o host Ansible e o host Windows.

* e. Tente usar outras opções de autenticação: Se o problema persistir, tente alterar a 
opção ansible_winrm_transport para 'credssp' ou 'kerberos' para ver se isso resolve o 
problema de conexão.

* f. Atualize as bibliotecas necessárias: Certifique-se de que todas as bibliotecas 
necessárias, como requests-ntlm, estejam instaladas e atualizadas no host Ansible.


## WINDOWS como Administrador no PowerShell

1. Execute:

```
Enable-PSRemoting -Force
```

2. Caso der erro, mude o tipo da categoria de rede para privada pois o WinRM não aceita pública.

```
Set-NetConnectionProfile -NetworkCategory Private
```

3. Execute novamente:

```
Enable-PSRemoting -Force
```

* deve retornar:
  - criar firewall rule corretamente
  - liberar 5985
  - SEM erro

4. Valide:

```
netsh advfirewall firewall show rule name=all | findstr /i 5985
```

* deve retorna:
  - LocalPort: 5985

* Ou

```
Test-NetConnection localhost -Port 5985
```

* Deve retorna:
  - TcpTestSucceeded : True

## LINUX

5. Teste:

```
nc -zv 192.168.0.202 5985
```

* Deve retornar:
  - succeeded
