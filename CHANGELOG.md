# Changelog

Todas as mudanças importantes deste projeto serão documentadas neste arquivo.

O formato é baseado em:
https://keepachangelog.com/pt-BR/1.1.0/

---

# [2.0.0] - 2026-05-26

## 🚀 Adicionado

- Estrutura modular completa para Windows
- Suporte ao Zabbix Agent clássico
- Suporte ao Zabbix Agent 2
- Sistema de backup automatizado
- Healthcheck automatizado
- Fluxo de validação pós-instalação
- Detecção automática de versão instalada
- Detecção automática do tipo do agente
- Detecção automática do serviço instalado
- Upgrade automatizado entre versões
- Re-registro automático de serviço quebrado
- Remoção automática de serviços órfãos
- Remoção automática de chaves órfãs do EventLog
- Configuração automática de firewall Windows
- Controle granular via tags
- Melhor tratamento de upgrades
- Melhor tratamento de serviços Windows
- Melhor tratamento de processos presos
- Melhor organização modular das tasks

---

## 🔧 Alterado

- Refatoração completa da role
- Separação das tasks em módulos independentes:
  - version
  - backup
  - install
  - configure
  - register
  - firewall
  - service
  - healthcheck
  - validate
  - remove
- Melhor organização de includes/imports
- Melhor tratamento de serviços Windows
- Melhor controle de execução parcial
- Melhor fluxo de atualização do agente
- Melhor fluxo de backup antes de upgrades

---

## 🐛 Corrigido

- Problemas de upgrade entre versões
- Falhas no re-registro do serviço
- Problemas de remoção de serviço órfão
- Problemas de validação de versão
- Problemas em upgrades Agent → Agent2
- Falhas relacionadas ao EventLog
- Problemas de diretório inexistente
- Problemas no fluxo de instalação
- Problemas de remoção incompleta
- Problemas no restart do serviço
- Problemas relacionados ao WinRM
- Problemas de sincronização durante upgrade
- Falhas de detecção do binário instalado

---

# [1.0.0] - 2024-04-24

## 🚀 Inicial

- Instalação básica do Zabbix Agent
- Configuração do serviço
- Configuração do firewall
- Remoção básica do agente
- Suporte inicial ao Windows