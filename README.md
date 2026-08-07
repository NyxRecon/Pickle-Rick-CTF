![Pickle Rick](screenshots/pickle_rick_capa.png)
# Pickle-Rick-CTF
Write-up técnico do CTF Pickle Rick (TryHackMe), documentando enumeração, exploração web e escalada de privilégios em ambiente Linux.

## 📌 Informações da Máquina

| Item | Informação |
|---|---|
| Plataforma | TryHackMe |
| Sistema | Linux |
| Dificuldade | Easy |
| Objetivo | Exploração web e privilege escalation |
| Status | Completed ✅ |

---

## 🛠️ Ferramentas utilizadas

- Nmap
- Gobuster
- Linux Commands
- Browser

# 1. Reconhecimento

## Nmap
Durante a fase inicial de reconhecimento foi realizado um scan de portas.

```bash
nmap -sV -sC prickctf
```
# Foram encontrados os serviços:
```text
22/tcp open ssh
80/tcp open http
```

![Pickle Rick](screenshots/pag_inicial.png)
Aplicação web encontrada durante a fase de reconhecimento.
# Source Code Analysis
Analisando o código fonte da aplicação foi possível identificar o usuário  R1ckRul3s.
# Acesso via SSH
A partir da descoberta de credencial realizei uma tentativa de acesso via ssh (porta 22 aberta).
```bash
ssh R1ckRul3s@prickctf
```
O acesso via ssh é permitido apenas com uso de chave:
```bash
R1ckRul3s@prickctf: Permission denied (publickey).
```

# 2. Web Enumeration
Foi realizada uma enumeração de diretórios e arquivos utilizando Gobuster.
```bash
gobuster dir -u http://prickctf -w /usr/share/wordlists/dirb/common.txt -t 50 -x php,html,txt
```
Resultados relevantes:
```bash
assets               (Status: 301) [Size: 311] [--> http://prickctf/assets/]
denied.php           (Status: 302) [Size: 0] [--> /login.php]
index.html           (Status: 200) [Size: 1062]
index.html           (Status: 200) [Size: 1062]
login.php            (Status: 200) [Size: 882]
portal.php           (Status: 302) [Size: 0] [--> /login.php]
robots.txt           (Status: 200) [Size: 17]
robots.txt           (Status: 200) [Size: 17]
```
Durante a análise do arquivo:

robots.txt

foi encontrado o seguinte conteúdo:
```bash
REDACTED
```
Esse valor foi identificado como uma possível senha.

## 3. Authentication

![Pickle Rick](screenshots/login.png)

Após autenticação, foi identificado um painel de comandos:

portal.php


O painel permitia execução de comandos no servidor.

Teste realizado:

