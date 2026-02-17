---
layout: default
title: Linux Fundamentals
---

# Linux — Fundamentos Operacionais

## Objetivo da Trilha

Desenvolver fluidez operacional no Linux, compreendendo filesystem, permissões, serviços, rede, automação básica e práticas fundamentais de segurança.

---

## Metas

- Navegar com eficiência pelo sistema
- Gerenciar serviços e investigar falhas
- Administrar usuários e permissões
- Diagnosticar conectividade e portas
- Automatizar tarefas básicas
- Aplicar controles mínimos de segurança

---

## Domínio Prático

### 1) Exploração do Sistema e Navegação

**Objetivo:** mover-se com fluidez pelo filesystem e inspecionar arquivos.

#### Comandos e explicação

- `pwd` — mostra o diretório atual.
- `ls -la` — lista arquivos/diretórios (inclui ocultos) com detalhes de permissões/dono/tamanho.
- `cd <diretório>` — altera o diretório atual.
- `tree` — exibe a estrutura de pastas em formato de árvore (pode exigir instalação).
- `find /caminho -name "arquivo"` — busca arquivos/pastas por nome (e outros critérios).
- `grep -R "pattern" ~/` — procura recursivamente por um padrão dentro de arquivos no diretório informado.

#### Critério de conclusão

- Listar 5 arquivos úteis do sistema e explicar onde ficam:
  - Logs principais: `/var/log`
  - Configurações: `/etc`
  - Binários: `/bin`, `/usr/bin`
  - Diretórios de usuário: `/home`

---

### 2) Permissões, Usuários e Grupos

**Objetivo:** entender modos, owners e grupos e aplicar mudanças com segurança.

#### Comandos e explicação

- `id` — mostra UID, GID e grupos do usuário.
- `whoami` — mostra o usuário efetivo atual.
- `chmod u+x arquivo` — adiciona permissão de execução ao dono do arquivo.
- `chown usuario:grupo arquivo` — altera dono e grupo do arquivo/pasta.
- `umask` — mostra/define a máscara padrão de permissões para novos arquivos.
- `sudo visudo` — edita `sudoers` com validação para evitar quebrar permissões de sudo.

#### Exercício

- Criar usuário e grupo de teste e controlar acesso a uma pasta.

#### Critério de conclusão

- Tabela simples antes/depois com `ls -l` mostrando mudanças:
  - `ls -l` — lista permissões, dono, grupo, tamanho e data de modificação.

---

### 3) Serviços e Inicialização

**Objetivo:** gerenciar serviços e investigar falhas básicas.

#### Comandos e explicação

- `systemctl status <serviço>` — mostra status atual, PID, logs recentes e estado de carregamento.
- `systemctl start <serviço>` — inicia o serviço imediatamente.
- `systemctl enable <serviço>` — habilita inicialização do serviço no boot.
- `journalctl -u <serviço> --since "today"` — exibe logs do serviço desde o início do dia.

#### Exercício

- Habilitar e iniciar um serviço de exemplo e coletar logs de inicialização.

#### Critério de conclusão

- Screenshot do `systemctl status`
- Bloco de logs relevantes com 2–3 linhas comentadas (o que significam e por que importam)

---

### 4) Rede Básica e Diagnóstico

**Objetivo:** verificar conectividade e resolver nomes.

#### Comandos e explicação

- `ip a` — mostra interfaces e endereços IP.
- `ip r` — mostra tabela de rotas (inclui rota padrão).
- `ss -tulpn` — lista sockets/portas abertas e tenta mapear processos (exige permissão para ver tudo).
- `ping <host>` — testa conectividade ICMP com um destino.
- `curl -I exemplo.com` — faz requisição HTTP e retorna apenas headers.
- `dig A exemplo.com` — consulta DNS para registros do tipo A (IPv4).

#### Exercício

- Identificar qual processo está escutando em uma porta específica.

#### Critério de conclusão

- Mini-nota explicando:
  - IP local (a partir do `ip a`)
  - Rota padrão (a partir do `ip r`)
  - Serviço/processo na porta escolhida (a partir do `ss -tulpn`)

---

### 5) Manipulação de Textos e Shell Produtivo

**Objetivo:** editar, filtrar e encadear comandos.

#### Comandos e explicação

- `nano arquivo` — editor simples no terminal.
- `vim arquivo` — editor avançado no terminal.
- `head arquivo` — mostra as primeiras linhas do arquivo.
- `tail arquivo` — mostra as últimas linhas do arquivo.
- `sort arquivo` — ordena linhas do arquivo.
- `uniq` — remove duplicatas consecutivas (geralmente usado após `sort`).
- `awk '{print $1}'` — extrai/transforma campos (colunas) de texto.
- `sed 's/erro/falha/g'` — substitui padrões em texto.
- `|` — pipe: envia a saída de um comando para a entrada do próximo.
- `>` — redireciona saída para arquivo (sobrescreve).
- `>>` — redireciona saída para arquivo (anexa ao final).

#### Exercício

- Extrair erros de um log e gerar um Top 5 de mensagens mais frequentes.

#### Critério de conclusão

- Comando final usado e saída resumida (Top 5)

---

### 6) Automatização Mínima

**Objetivo:** escrever um script simples com tratamento básico de erro.

#### Tarefas e explicação

- Script Bash que:
  - verifica status de serviço (`systemctl is-active <serviço>`)
  - registra status com timestamp (`date`) em um arquivo
  - retorna código de saída coerente (sucesso/erro)

#### Critério de conclusão

- Script no repositório
- Tornar executável: `chmod +x script.sh` — adiciona permissão de execução
- Rodar com sucesso e validar o arquivo de log gerado

---

### 7) Segurança de Base

**Objetivo:** checar permissões sensíveis e histórico.

#### Tarefas e explicação

- Revisar `sudoers` via `sudo visudo` — reduz risco de travar permissões de admin.
- Checar `~/.ssh` — diretório de chaves e configs SSH do usuário.
- Ajustar permissões de chave privada para `600`:
  - `chmod 600 ~/.ssh/id_rsa` — restringe leitura/escrita apenas ao dono.
- Revisar histórico com consciência:
  - `history` — exibe comandos executados no shell.

#### Critério de conclusão

- Checklist com 5 itens de hardening aplicados e justificados (1 linha por item)

---

### 8) OverTheWire — Warm-up

**Objetivo:** praticar lógica e comandos sob pressão.

#### Tarefas

- Completar 3 níveis do Bandit e registrar o comando-chave de cada nível.

#### Critério de conclusão

- Lista no formato:
  - `Nível → comando principal → observação`

---
