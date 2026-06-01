<!---
# ================================================================
Projeto: ansible-zabbix-agent-windows
---
Descrição: Projeto Ansible modular para instalar, configurar,
validar, atualizar e remover o Zabbix Agent em hosts Windows.
---
Autor..........: Glauber GF (mcnd2)
Data...........: 24/04/2024
Atualizado.....: 28/05/2026
# ================================================================
-->

# Zabbix Agent Windows com Ansible

![Image](https://github.com/glaubergf/ansible-zabbix-agent-windows/blob/main/images/hosts_zabbix.png)

![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)


# 📜 Sobre o Projeto

Este projeto automatiza a instalação, atualização, configuração, validação e remoção do **Zabbix Agent** em ambientes **Microsoft Windows** utilizando **Ansible**.

O projeto foi totalmente refatorado para uma arquitetura modular, permitindo:

- Instalação limpa
- Upgrade automático entre versões
- Backup automático antes de atualização
- Registro e re-registro automático do serviço
- Configuração automática do firewall
- Healthcheck da porta do agente
- Validação pós-instalação
- Execução granular via tags


# 📊 Sobre o Zabbix Agent

O **[Zabbix Agent](https://www.zabbix.com/documentation/current/pt/manual/concepts/agent)** é responsável pela coleta de métricas e informações do sistema operacional monitorado.

O projeto suporta:

- Zabbix Agent clássico
- Zabbix Agent 2


# 🤖 Sobre o Ansible

O **[Ansible](https://docs.ansible.com/ansible/latest/index.html)** é uma ferramenta open source para automação, provisionamento e gerenciamento de configuração.

Com este projeto é possível:

- Automatizar deploy do Zabbix Agent em Windows
- Padronizar ambientes
- Automatizar upgrades
- Reduzir falhas operacionais
- Executar remoção limpa do agente


# 🧩 Tecnologias Utilizadas

![Ansible](https://img.shields.io/badge/Ansible-EE0000?logo=ansible&logoColor=white&style=for-the-badge)

- [Ansible](https://www.ansible.com/) — Automação e gerenciamento de configuração.

![Windows](https://img.shields.io/badge/Windows-0078D6?logo=windows&logoColor=white&style=for-the-badge)

- [Microsoft Windows](https://www.microsoft.com/windows/) — Sistema Operacional.

![Zabbix](https://img.shields.io/badge/Zabbix-D40000?logo=zabbix&logoColor=white&style=for-the-badge)

- [Zabbix](https://www.zabbix.com/) — Plataforma de monitoramento.


# 🪟 Sistemas Operacionais Testados

| Sistema | Ambiente | Versão | Status |
|---|---|---|---|
| ![Windows 11](https://img.shields.io/badge/Windows%2011-0078D6?logo=windows&logoColor=white&style=for-the-badge) | VM (KVM) | 24H2 | ✅ |
| ![Windows 11](https://img.shields.io/badge/Windows%2011-0078D6?logo=windows&logoColor=white&style=for-the-badge) | Máquina Física | 23H2 | ✅ |
| ![Windows 10](https://img.shields.io/badge/Windows%2010-0078D6?logo=windows&logoColor=white&style=for-the-badge) | Máquina Física | 22H2 | ✅ |
| ![Windows Server](https://img.shields.io/badge/Windows%20Server-0078D6?logo=windows&logoColor=white&style=for-the-badge) | VM (Proxmox) | 2022 | ✅ |


# 🚀 Funcionalidades

## ✅ Instalação Automatizada

- Download automático do pacote oficial
- Extração automática do ZIP
- Instalação do serviço
- Inicialização automática


## 🔄 Upgrade Automatizado

O projeto detecta automaticamente:

- versão instalada
- tipo do agente instalado
- status do serviço

Durante upgrades:

- realiza backup automático
- remove serviço quebrado automaticamente
- re-registra o serviço
- mantém a configuração
- valida o funcionamento após atualização


## 🛡️ Firewall Automático

O projeto cria automaticamente:

- regra de entrada TCP 10050
- regra identificada para Zabbix Agent


## ❤️ Healthcheck

Após instalação ou upgrade:

- valida serviço
- valida porta TCP 10050
- valida versão instalada
- valida inicialização automática


# 🛠️ Pré-requisitos

## Controlador Ansible

- Linux/macOS/WSL
- Ansible instalado
- Collections:
  - `ansible.windows`
  - `community.windows`

Instalação:

```bash
ansible-galaxy collection install ansible.windows
ansible-galaxy collection install community.windows
```


## Hosts Windows

- WinRM habilitado
- PowerShell disponível
- Usuário administrador
- Firewall liberando WinRM


# ⚠️ Importante Sobre WinRM

O Ansible utiliza WinRM para comunicação com hosts Windows.

O host precisa possuir:

- WinRM habilitado
- Usuário administrador
- Porta liberada
- Permissões remotas


# 📂 Estrutura do Projeto

```bash
ansible-zabbix-agent-windows
├── ansible.cfg
├── CHANGELOG.md
├── group_vars
│   └── all.yml
├── images
│   ├── dashboard_zabbix.png
│   └── hosts_zabbix.png
├── inventory
│   └── hosts.yml
├── LICENSE
├── main.yml
├── notes
│   └── WinRM.txt
├── README.md
└── roles
    └── zabbix-agent-windows
        ├── defaults
        │   └── main.yml
        ├── handlers
        │   └── main.yml
        ├── tasks
        │   ├── backup.yml
        │   ├── configure.yml
        │   ├── firewall.yml
        │   ├── healthcheck.yml
        │   ├── install.yml
        │   ├── main.yml
        │   ├── register.yml
        │   ├── remove.yml
        │   ├── service.yml
        │   ├── validate.yml
        │   └── version.yml
        └── templates
            └── zabbix_agent.conf.j2
```


# 🚀 Fluxo de Funcionamento

A role executa automaticamente:

1. Detecção do agente instalado
2. Coleta da versão instalada
3. Backup da instalação atual
4. Parada do serviço
5. Remoção segura do diretório antigo
6. Download da nova versão
7. Instalação do agente
8. Configuração do arquivo `.conf`
9. Registro do serviço
10. Configuração do firewall
11. Inicialização do serviço
12. Healthcheck da porta
13. Validação final


# 💾 Sistema de Backup

Antes de upgrades:

- o diretório atual é salvo automaticamente
- backups possuem timestamp
- configuração anterior é preservada

Exemplo:

```powershell
C:\Programs Files\Zabbix Agent-backup-7.0.26-20260526T010538
```


# 🔍 Validação Automática

O projeto valida automaticamente:

| Verificação | Status |
|---|---|
| Serviço registrado | ✅ |
| Serviço iniciado | ✅ |
| Startup automático | ✅ |
| Porta 10050 | ✅ |
| Binário instalado | ✅ |
| Versão instalada | ✅ |


# 🏷️ Tags Disponíveis

| Tag | Descrição |
|---|---|
| `zbx-agt-win` | Fluxo completo |
| `zbx-agt-win-version` | Apenas detecção de versão |
| `zbx-agt-win-backup` | Apenas backup |
| `zbx-agt-win-install` | Apenas instalação |
| `zbx-agt-win-configure` | Apenas configuração |
| `zbx-agt-win-register` | Apenas registro do serviço |
| `zbx-agt-win-firewall` | Apenas firewall |
| `zbx-agt-win-service` | Apenas serviço |
| `zbx-agt-win-healthcheck` | Apenas healthcheck |
| `zbx-agt-win-validate` | Apenas validação |
| `zbx-agt-win-remove` | Apenas remoção |


# ▶️ Execução do Projeto

## Clone o repositório

```bash
git clone https://github.com/glaubergf/ansible-zabbix-agent-windows.git

cd ansible-zabbix-agent-windows
```


## Instalação Completa

```bash
ansible-playbook -i inventory/hosts.yml main.yml -t zbx-agt-win
```


## Remover Zabbix Agent

```bash
ansible-playbook -i inventory/hosts.yml main.yml \
-e zabbix_agent_state=absent \
-t zbx-agt-win
```


## Apenas validação

```bash
ansible-playbook -i inventory/hosts.yml main.yml \
-t zbx-agt-win-validate
```


## Apenas healthcheck

```bash
ansible-playbook -i inventory/hosts.yml main.yml \
-t zbx-agt-win-healthcheck
```


## Apenas configuração

```bash
ansible-playbook -i inventory/hosts.yml main.yml \
-t zbx-agt-win-configure
```


## Modo simulação (Dry Run)

```bash
ansible-playbook -i inventory/hosts.yml main.yml \
-t zbx-agt-win \
--check
```


# 🧠 Detecção Automática

O projeto detecta automaticamente:

- tipo do agente
- versão instalada
- status do serviço
- modo de inicialização
- existência do binário
- existência da configuração


# 🧹 Remoção Completa

A remoção elimina:

- serviço Windows
- regras de firewall
- diretório de instalação
- chaves órfãs do EventLog
- serviços quebrados do SCM


# 📑 Histórico de Alterações

Todas as mudanças importantes deste projeto são documentadas em:

- [CHANGELOG.md](CHANGELOG.md)


# 🤝 Contribuições

Contribuições são bem-vindas.


# 📜 Licença

Este projeto está licenciado sob os termos da:

**GNU General Public License v3**

https://www.gnu.org/licenses/gpl-3.0.html


# 🏛️ Aviso Legal

```text
Copyright (c) 2024-2026 Glauber GF (mcnd2)

Este programa é software livre: você pode redistribuí-lo e/ou modificá-lo
sob os termos da GNU General Public License conforme publicada pela
Free Software Foundation, na versão 3 da Licença ou posterior.

Este programa é distribuído na esperança de ser útil,
mas SEM NENHUMA GARANTIA.

Veja a Licença Pública Geral GNU para mais detalhes.
```