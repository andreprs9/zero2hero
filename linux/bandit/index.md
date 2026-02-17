---
layout: default
title: Linux Fundamentals
permalink: /linux/bandit/
---

# OverTheWire Bandit — Níveis Iniciais

## Contexto

O objetivo desta fase inicial foi realizar a conexão via SSH ao ambiente do OverTheWire (Bandit) e resolver os primeiros desafios utilizando comandos básicos de Linux e técnicas fundamentais de enumeração.

---

## Conexão SSH

**Alvo:**

- Host: `bandit.labs.overthewire.org`
- Porta: `2220`
- Usuário inicial: `bandit0`

### Comando utilizado

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

### Explicação

- `ssh` → inicia conexão remota segura.
- `bandit0@host` → define usuário e servidor.
- `-p 2220` → especifica porta customizada.

---

## Enumeração Inicial do Diretório

Após o login, foi realizada a listagem do diretório atual:

```bash
ls -la
```

### Explicação

- `-l` → exibe permissões, dono, grupo e tamanho.
- `-a` → mostra arquivos ocultos.

### Objetivo

- Identificar arquivos disponíveis.
- Verificar permissões e estrutura do diretório.
- Localizar o arquivo contendo a senha do próximo nível.

---

## Enumeração do Sistema com `hostnamectl`

```bash
hostnamectl
```

### Objetivo

Enumerar informações do sistema, incluindo:

- Nome do host
- Sistema operacional
- Versão do kernel
- Arquitetura

### Importância

- Identificação de versão do sistema
- Reconhecimento do ambiente
- Possível identificação de vetores dependentes de versão

---

## Arquivo com Nome "-"

O enunciado indicava que a senha estava em um arquivo chamado:

```
-
```

### Problema

No Linux, qualquer argumento iniciado com `-` é interpretado como flag do comando.

Tentativa incorreta:

```bash
cat -
```

O sistema interpreta como entrada padrão (stdin).

---

## Solução

### Método 1

```bash
cat -- -
```

### Método 2

```bash
cat ./-
```

### Explicação

- `--` → indica o fim das opções do comando.
- `./-` → força interpretação como caminho relativo.

---

## Arquivo com Espaços no Nome

O próximo desafio envolvia um arquivo cujo nome continha espaços.

Tentativa incorreta:

```bash
cat file name with spaces
```

O shell interpreta cada espaço como separador de argumento.

---

## Soluções

### Escapar espaços

```bash
cat file\ name\ with\ spaces
```

### Usar aspas

```bash
cat "file name with spaces"
```

Ambas fazem o shell tratar o nome como um único argumento.

---

## Arquivo Oculto no Diretório `inhere`

Foi necessário localizar um arquivo oculto dentro do diretório `inhere`.

Listagem padrão:

```bash
ls
```

Não exibe arquivos ocultos.

---

## Solução

```bash
ls -la
```

### Explicação

- `-a` → lista arquivos ocultos.
- `-l` → mostra detalhes de permissões e propriedades.

Após identificar o nome correto:

```bash
cat <nome_do_arquivo>
```

---

# Conceitos Reforçados

- Interpretação de flags pelo shell.
- Uso de `--` para finalizar parsing de opções.
- Tratamento de arquivos com nomes especiais.
- Uso correto de aspas e escape em nomes com espaços.
- Importância da enumeração completa com `ls -la`.

---

# Conclusão

Os primeiros níveis do Bandit reforçam fundamentos essenciais:

- Entendimento do comportamento do shell.
- Enumeração básica eficiente.
- Manipulação correta de arquivos com nomes incomuns.
- Compreensão do parsing de argumentos no Linux.

Esses conceitos formam a base para troubleshooting, auditoria e segurança em ambientes Linux.
