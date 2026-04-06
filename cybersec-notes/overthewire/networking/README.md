# Networking (angle sécurité) — Notes THM

---

## Nmap — Scanner de ports

```bash
# Scans de base
nmap cible                    # 1000 ports TCP principaux
nmap -p- cible                # Tous les 65535 ports
nmap -p 22,80,443 cible       # Ports spécifiques

# Détection et fingerprinting
nmap -sV cible                # Version des services
nmap -sC cible                # Scripts NSE par défaut
nmap -O cible                 # Détection de l'OS
nmap -A cible                 # Tout en un (OS+version+scripts)

# Types de scan
nmap -sS cible                # SYN scan (furtif, nécessite root)
nmap -sU cible                # UDP scan (lent mais utile)
nmap -sn 192.168.1.0/24      # Ping sweep — découvrir les hôtes

# Performance
nmap -T4 cible                # Rapide (T1=furtif → T5=agressif)

# Sauvegarder les résultats
nmap -oN scan.txt cible       # Format texte normal
nmap -oA scan cible           # Tous les formats (normal/xml/grepable)
```

## Wireshark — Filtres utiles

```
ip.addr == 192.168.1.1           # Trafic vers/depuis une IP
tcp.port == 80                    # Trafic HTTP
http                              # Tout le trafic HTTP
http.request.method == "POST"     # Requêtes POST uniquement
dns                               # Requêtes DNS seulement
tcp.flags.syn == 1                # Paquets SYN (nouvelles connexions)
!(arp or dns or icmp)             # Exclure le bruit de fond
```

## Ce que j'ai appris

- [ ] Compléter au fur et à mesure des rooms
