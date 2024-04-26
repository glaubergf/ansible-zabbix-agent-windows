---
Projeto: ansible-zabbix-agent-windows
Descrição: Esse projeto tem o objetivo de instalar e configurar o pacote "zabbix-agent" em
           sistema Windows.
Autor: Glauber GF (mcnd2)
Data: 2024-04-24
---

# Instalar e Configurar o "Zabbix Agent" com o Ansible em sistemas Windows.

![Image](https://github.com/glaubergf/ansible-zabbix-agent/blob/main/images/hosts_zabbix.png)

O objetivo desse projeto é executar com o Ansible a automatização para instalar e configurar o Zabbix Agent em sistema baseado no Windows 10 e Windows 11.

O **[Zabbix Agent](https://www.zabbix.com/documentation/6.4/pt/manual/guides/monitor_linux?hl=Zabbix%2Cagent)** é o processo responsável pela coleta de dados. Ele é um componente essencial do Zabbix, que é uma plataforma de monitoramento de rede e sistemas. O Zabbix Agent é instalado nos dispositivos que você deseja monitorar e coleta dados específicos sobre esses dispositivos para enviar de volta ao servidor Zabbix.

Existem dois modos principais de operação para o Zabbix Agent:

* Modo Passivo:

  Neste modo, o Zabbix Agent espera passivamente por solicitações do servidor Zabbix. O servidor envia uma solicitação ao agente em intervalos regulares para obter dados de monitoramento, e o agente responde com as informações solicitadas. Este modo é mais comum em ambientes onde a comunicação de saída do dispositivo é limitada, como em firewalls ou em dispositivos de rede.

* Modo Ativo:

  Neste modo, o Zabbix Agent envia ativamente os dados de monitoramento para o servidor Zabbix em intervalos regulares. O agente inicia a comunicação com o servidor e envia os dados sem que o servidor precise solicitar. Esse modo é mais adequado para dispositivos com comunicação de saída permitida e oferece uma abordagem mais proativa para o monitoramento.

Em resumo, o Zabbix Agent é responsável por coletar dados de monitoramento nos dispositivos e enviá-los de volta ao servidor Zabbix, e pode operar tanto no modo passivo quanto no modo ativo, dependendo das necessidades e restrições do ambiente de rede.

O **[Ansible](https://docs.ansible.com/ansible/latest/getting_started/index.html)** fornece automação de código aberto que reduz a complexidade e funciona em qualquer lugar. Usar o Ansible permite automatizar praticamente qualquer tarefa. A organização e estruturação do projeto Ansible são fundamentais para garantir a eficiência e a manutenção do código.

Atualmente o Ansible pertence a **[Red Hat](https://www.redhat.com/pt-br/technologies/management/ansible)**.

Pressupondo que você já tenha o **Ansible** e as suas dependências instaladas, para executar o projeto, faça o clone do mesmo e em seguida certifique-se que esteja dentro do diretório raíz do projeto. Altere os dados relacionados a seu ambiente e de acordo com as suas necessidades.

Para instalar e configurar o zabbix agent, role "zabbix-agent-windows", execute o comando seguido com a opção "-t" ( --tags ), nome da "tag" que foi dado nas tarefas da role.

```
ansible-playbook -i host main.yml -t zbx-agt
```

Para saber mais opções do Ansible, execute com a opção "-h" ( --help) para mostrar a ajuda para o uso de cada opção.

```
ansible --help
```

## Playbook

O **Playbook** define uma série de **roles** que serão aplicadas no alvo (hosts). Cada role é associada a uma **tag** específica, permitindo que as **tarefas** sejam executadas de forma seletiva com base nessas tags.

Há uma única **roles** nesse projeto que é para instalar o zabbix agent (_zabbix-agent-windows_).

Segue as especificações das **tarefas** da role.

### zabbix-agent-windows

* _zabbix_agent_windows.yml_

Executa uma série de tarefas para instalar e configurar o Zabbix Agent em sistemas Windows. Segue resumo de cada tarefa:

    -> Baixando o pacote Zabbix Agent:
    Faz o download do pacote do Zabbix Agent e o salva no diretório temporário do Windows.
    
    -> Descompactando o arquivo:
    Extrai o conteúdo do arquivo ZIP baixado para o diretório de instalação do Zabbix Agent, excluindo o arquivo ZIP após a extração.

    -> Registrando o serviço Zabbix Agent:
    Registra o Zabbix Agent como um serviço do Windows.

    -> Iniciando o serviço Zabbix Agent:
    Inicia o serviço recém-registrado.
    
    -> Fazendo backup do arquivo de configuração:
    Faz uma cópia de backup do arquivo de configuração do Zabbix Agent.
    
    -> Limpando o conteúdo do arquivo de configuração:
    Limpa o conteúdo do arquivo de configuração do Zabbix Agent ou cria um novo se não existir.
    
    -> Coletando informações do sistema operacional:
    Obtém informações sobre o sistema operacional Windows.

    -> Exibindo versão do sistema operacional:
    Exibe a versão do sistema operacional Windows.

    -> Extraindo apenas a versão do Windows:
    Processa e extrai a versão específica do Windows a partir das informações coletadas.
    
    -> Coletando informações do hardware do sistema:
    Obtém informações sobre o hardware do sistema.

    -> Verificando o tipo do hardware:
    Determina se o hardware é da marca Dell.
    
    -> Definindo Hostname com base na versão do Windows e hardware:
    Define o hostname com base na versão do Windows e no tipo de hardware.
    
    -> Exibindo o Hostname:
    Exibe o hostname configurado.

    -> Editando o arquivo de configuração do Zabbix Agent:
    Adiciona ou atualiza configurações no arquivo de configuração do Zabbix Agent, como o caminho do arquivo de log, os endereços do servidor Zabbix e o hostname.
    
    -> Parando o serviço Zabbix Agent:
    Interrompe temporariamente o serviço do Zabbix Agent.
    
    -> Aguardando:
    Pausa a execução por 10 segundos.
    
    -> Iniciando novamente o serviço Zabbix Agent:
    Inicia o serviço do Zabbix Agent após a pausa.

A última tarefa que está comentada, é destinada à remoção do serviço Zabbix Agent.

# Licença

**GNU General Public License** (_Licença Pública Geral GNU_), **GNU GPL** ou simplesmente **GPL**.

[GPLv3](https://www.gnu.org/licenses/gpl-3.0.html)

------

Copyright (c) 2024 Glauber GF (mcnd2)

Este programa é um software livre: você pode redistribuí-lo e/ou modificar
sob os termos da GNU General Public License conforme publicada por
a Free Software Foundation, seja a versão 3 da Licença, ou
(à sua escolha) qualquer versão posterior.

Este programa é distribuído na esperança de ser útil,
mas SEM QUALQUER GARANTIA; sem mesmo a garantia implícita de
COMERCIALIZAÇÃO ou ADEQUAÇÃO A UM DETERMINADO FIM. Veja o
GNU General Public License para mais detalhes.

Você deve ter recebido uma cópia da Licença Pública Geral GNU
junto com este programa. Caso contrário, consulte <https://www.gnu.org/licenses/>.

*

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <https://www.gnu.org/licenses/>