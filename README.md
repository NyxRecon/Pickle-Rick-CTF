
# Pickle-Rick-CTF
Write-up técnico do CTF Pickle Rick (TryHackMe), documentando enumeração, exploração web e escalada de privilégios em ambiente Linux.

# 🥒 TryHackMe — Pickle Rick

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
#Foram encontrados os serviços:
22/tcp open ssh
80/tcp open http




