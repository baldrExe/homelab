# Protocoles réseau — Référence Network+

## Modèle OSI vs TCP/IP

```
OSI                     TCP/IP          Exemples de protocoles
──────────────────────────────────────────────────────────────
7 - Application    ┐
6 - Présentation   ├── Application     HTTP, HTTPS, DNS,
5 - Session        ┘                   SMTP, FTP, SSH, DHCP

4 - Transport      ──── Transport      TCP, UDP

3 - Réseau         ──── Internet       IP, ICMP, ARP

2 - Liaison        ┐
1 - Physique       ┘   Accès réseau    Ethernet, Wi-Fi
```

## Ports à connaître par cœur (Network+)

| Port  | Protocole | Usage                          |
|-------|-----------|--------------------------------|
| 20/21 | FTP       | Transfert de fichiers          |
| 22    | SSH       | Accès distant sécurisé         |
| 23    | Telnet    | Accès distant non sécurisé     |
| 25    | SMTP      | Envoi d'emails                 |
| 53    | DNS       | Résolution de noms             |
| 67/68 | DHCP      | Attribution IP automatique     |
| 80    | HTTP      | Web non chiffré                |
| 110   | POP3      | Réception emails               |
| 143   | IMAP      | Réception emails (sync)        |
| 443   | HTTPS     | Web chiffré (TLS)              |
| 3389  | RDP       | Bureau à distance Windows      |

## TCP vs UDP

| Critère     | TCP                             | UDP                  |
|-------------|---------------------------------|----------------------|
| Connexion   | Orienté connexion (handshake)   | Sans connexion       |
| Fiabilité   | Accusés de réception            | Pas de garantie      |
| Vitesse     | Plus lent                       | Plus rapide          |
| Usage       | HTTP, SSH, FTP, email           | DNS, VoIP, streaming |

## 3-way handshake TCP

```
Client          Serveur
  │──── SYN ────▶│   "Je veux me connecter"
  │◀─── SYN-ACK ─│   "OK, je t'entends"
  │──── ACK ────▶│   "C'est parti"
  │   [données]  │
```

## Commandes de diagnostic réseau

```bash
# Connectivité
ping 8.8.8.8
ping -c 4 8.8.8.8          # Linux : limiter à 4 paquets

# Traçage de route
traceroute 8.8.8.8         # Linux / macOS
tracert 8.8.8.8            # Windows

# DNS
nslookup google.com
dig google.com             # Plus détaillé

# Ports et connexions
netstat -an                # Toutes les connexions
ss -tuln                   # Ports en écoute (Linux, moderne)

# Config réseau
ip addr show               # Linux
ipconfig /all              # Windows
```
