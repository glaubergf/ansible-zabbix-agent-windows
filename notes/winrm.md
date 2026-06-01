# WinRM (Windows Remote Management)

O WinRM é um serviço da Microsoft que permite administrar computadores Windows remotamente 
usando protocolos padrão de gerenciamento, principalmente o WS-Management (WS-Man) baseado 
em HTTP/HTTPS.

### Na prática:

* executar comandos remotamente;
* automatizar administração de servidores;
* gerenciar máquinas via scripts;
* permitir ferramentas como PowerShell Remoting;
* integrar sistemas de monitoramento e automação.

O WinRM funciona como a "porta de comunicação" para administração remota no Windows.

## Exemplos comuns de uso

### PowerShell remoto

Abrir uma sessão remota em outro computador Windows:

```
Enter-PSSession -ComputerName SERVIDOR01
```

Ou executar comandos remotamente:

```
Invoke-Command -ComputerName SERVIDOR01 -ScriptBlock {
    Get-Service
}
```

Isso depende do WinRM estar habilitado.

## Portas usadas

Por padrão:

* **5985** → HTTP
* **5986** → HTTPS

Versões antigas podiam usar as portas 80/443.

## Como habilitar

No Windows:

```
Enable-PSRemoting
```

Esse comando:

* inicia o serviço WinRM;
* cria regras de firewall;
* configura listeners HTTP.

## Segurança

O WinRM suporta:

* autenticação Kerberos;
* NTLM;
* certificados;
* criptografia via HTTPS.

Em ambientes corporativos, normalmente é usado junto com:

* Active Directory;
* automação;
* ferramentas de DevOps.

## Ferramentas que usam WinRM

Algumas tecnologias dependem dele:

* PowerShell
* Ansible (para gerenciar Windows)
* System Center Configuration Manager
* Windows Admin Center

## Diferença entre WinRM e RDP

| WinRM	| RDP 
|-------|-----
Administração via comandos/scripts | Acesso gráfico remoto
Automação	| Uso interativo
Leve | Mais pesado
Muito usado por admins/DevOps	| Muito usado por suporte técnico

## Quando você verá WinRM na prática

* Administração de servidores Windows;
* Automação de infraestrutura;
* Ambientes corporativos;
* Pentest e segurança ofensiva;
* Gerenciamento remoto sem interface gráfica.

A documentação oficial da Microsoft está em:

**[Microsoft WinRM Documentation](https://learn.microsoft.com/pt-br/windows/win32/WinRM/portal)**